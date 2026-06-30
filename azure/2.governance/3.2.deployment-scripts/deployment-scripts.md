# Azure Deployment Scripts

**Azure Deployment Scripts** let an ARM template or Bicep deployment execute an **Azure CLI Bash script** or an **Azure PowerShell script** as part of infrastructure deployment.

It is not a long-running application service. It is an Azure Resource Manager resource:

```text
Microsoft.Resources/deploymentScripts
```

The current documented resource API version is `2023-08-01`. ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/templates/microsoft.resources/deploymentscripts 'Microsoft.Resources/deploymentScripts - Bicep, ARM template & Terraform AzAPI reference | Microsoft Learn'))

## Why do we need it?

Bicep and ARM templates are declarative:

> “Create this storage account, network, AKS cluster, or Key Vault.”

However, some operations cannot be expressed easily as normal Azure resources, especially:

- Data-plane operations
- Seeding a database
- Copying blobs
- Creating Microsoft Entra ID objects
- Generating certificates or SSH keys
- Calling an external API
- Running post-deployment configuration
- Looking up information and returning it to Bicep

Deployment Scripts bridge this gap by allowing imperative commands inside a declarative deployment. ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-script-bicep?utm_source=chatgpt.com 'Use deployment scripts in Bicep - Azure Resource Manager | Microsoft Learn'))

## How it works

When ARM deploys a `deploymentScripts` resource:

```text
Bicep/ARM deployment
        │
        ▼
Deployment Script resource
        │
        ├── Creates an Azure Container Instance
        ├── Creates or uses a Storage Account
        ├── Runs Azure CLI or Azure PowerShell
        ├── Saves logs and output
        └── Returns output to Bicep/ARM
```

Azure uses:

- **Azure Container Instances** to execute the script.
- **Azure Storage** to hold scripts, logs, stdout and execution results.
- Optionally, a **user-assigned managed identity** to authenticate the script to Azure. ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-script-bicep 'Use deployment scripts in Bicep - Azure Resource Manager | Microsoft Learn'))

## Simple Bicep example

```bicep
param location string = resourceGroup().location
param environmentName string = 'uat'

resource setupScript 'Microsoft.Resources/deploymentScripts@2023-08-01' = {
  name: 'configure-${environmentName}'
  location: location
  kind: 'AzureCLI'

  properties: {
    azCliVersion: '2.59.0'

    scriptContent: '''
      echo "Configuring environment..."

      RESULT="Configuration completed for $ENVIRONMENT_NAME"

      jq -n \
        --arg message "$RESULT" \
        '{"message": $message}' > $AZ_SCRIPTS_OUTPUT_PATH
    '''

    environmentVariables: [
      {
        name: 'ENVIRONMENT_NAME'
        value: environmentName
      }
    ]

    cleanupPreference: 'OnSuccess'
    retentionInterval: 'PT1H'
    timeout: 'PT30M'
  }
}

output scriptResult string = setupScript.properties.outputs.message
```

The deployment output would contain something similar to:

```text
Configuration completed for uat
```

For Azure CLI scripts, outputs must be written as JSON to:

```bash
$AZ_SCRIPTS_OUTPUT_PATH
```

For Azure PowerShell, outputs are assigned to:

```powershell
$DeploymentScriptOutputs
```

Azure then exposes these results through `deploymentScript.properties.outputs`. ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-script-bicep 'Use deployment scripts in Bicep - Azure Resource Manager | Microsoft Learn'))

## Authentication and permissions

There are two different identities to understand.

### 1. Deployment identity

This is the identity running the Bicep deployment, such as an Azure DevOps service principal.

It needs permission to create:

- `Microsoft.Resources/deploymentScripts`
- Azure Container Instances
- Supporting Storage resources

### 2. Script identity

This is the identity used **inside the script** when running commands such as:

```bash
az keyvault secret set
az storage blob upload
az aks command invoke
```

The recommended option is a **user-assigned managed identity**:

```bicep
identity: {
  type: 'UserAssigned'
  userAssignedIdentities: {
    '${scriptIdentity.id}': {}
  }
}
```

Only user-assigned managed identity is currently supported directly on the deployment script identity property. The identity should receive only the permissions required by the script. ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-script-bicep 'Use deployment scripts in Bicep - Azure Resource Manager | Microsoft Learn'))

## Cleanup options

`cleanupPreference` controls when Azure removes the supporting container instance and storage resources.

| Value          | Meaning                                                                   |
| -------------- | ------------------------------------------------------------------------- |
| `Always`       | Remove supporting resources after execution, whether it succeeds or fails |
| `OnSuccess`    | Remove them only when the script succeeds                                 |
| `OnExpiration` | Keep them until `retentionInterval` expires                               |

For troubleshooting, `OnExpiration` is useful because it gives you time to inspect logs and output files. The documented default is `Always`. ([Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-script-bicep 'Use deployment scripts in Bicep - Azure Resource Manager | Microsoft Learn'))

Example:

```bicep
cleanupPreference: 'OnExpiration'
retentionInterval: 'PT2H'
```

This keeps the supporting resources for two hours.

## Important behaviour

Deployment Scripts are treated as ARM resources. Azure does not necessarily execute the same unchanged script every time you redeploy.

To intentionally force another execution, change the `forceUpdateTag` value:

```bicep
forceUpdateTag: utcNow()
```

Use that carefully because it makes the script execute on every deployment.

A safer pipeline-driven pattern is:

```bicep
param deploymentRunId string

forceUpdateTag: deploymentRunId
```

Then pass the Azure DevOps build number:

```text
deploymentRunId = $(Build.BuildNumber)
```

## When to use it

Use Deployment Scripts for a **small deployment-time action** that cannot be represented cleanly in Bicep, for example:

```text
Create infrastructure → run one configuration action → return result
```

Do not use it as a replacement for:

- Azure DevOps pipeline stages
- Long-running jobs
- Application deployments
- Complex database migration frameworks
- Configuration management
- General automation platforms

For your enterprise pipelines, use Bicep for infrastructure and Deployment Scripts only for exceptional post-provisioning operations that must be part of the ARM deployment transaction.

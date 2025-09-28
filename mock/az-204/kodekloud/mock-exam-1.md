# 📋 Mock Exam 1

## ⁉️ Q50

<div align="left">
  <img src="image/mock-exam-1/1759060714398.png" alt="1759060714398" style="width: 60%; border-radius: 10px; border: 2px solid white;">
</div>

---

> 👉🏻 **Explanation**

---

## ⁉️ Q49

<div align="left">
  <img src="image/mock-exam-1/1759060809391.png" alt="1759060809391" style="width: 60%; border-radius: 10px; border: 2px solid white;">
</div>

---

> 👉🏻 **Explanation**

---

## ⁉️ Q48

<div align="left">
  <img src="image/mock-exam-1/1759061120088.png" alt="1759061120088" style="width: 60%; border-radius: 10px; border: 2px solid white;">
</div>

---

> 👉🏻 **Explanation**
>
> ```bash
> az cosmosdb create \
>   -n $myCosmosAccountName \
>   -g myResourceGroup \
>   --capabilities EnableTable \
>   --default-consistency-level Eventual
>
> az cosmosdb table create \
>   -a $myCosmosAccountName \
>   -g myResourceGroup \
>   -n $tableName \
>   --throughput 400
> ```

---

## ⁉️ Q45

<div align="left">
  <img src="image/mock-exam-1/1759061517581.png" alt="1759061517581" style="width: 60%; border-radius: 10px; border: 2px solid white;">
</div>

---

> 👉🏻 **Explanation**  
> To delay the processing of messages in an Azure Service Bus queue, the `ScheduledEnqueueTimeUtc` property is used. This property schedules a message to be enqueued and available for processing at a future date and time, fulfilling the requirement to move messages to the active state only after a set period. The other options like Lock and timeout do not directly control when a message becomes available for processing.

---

## ⁉️ Q44

<div align="left">
  <img src="image/mock-exam-1/1759062099314.png" alt="1759062099314" style="width: 60%; border-radius: 10px; border: 2px solid white;">
</div>

---

> 👉🏻 **Explanation**  
> The `Impact` feature in Application Insights helps you analyze how different factors, like page load time, impact the user experience, including conversion rates. This makes it ideal for understanding the correlation between performance and user behavior.

---

## ⁉️ Q43

<div align="left">
  <img src="image/mock-exam-1/1759062525819.png" alt="1759062525819" style="width: 60%; border-radius: 10px; border: 2px solid white;">
</div>

---

> 👉🏻 **Explanation**
>
> **✅ the answer:**
> The two correct options are:
> 1-
>
> ```powershell
> $certificatepolicy = New-AzKeyVaultCertificatePolicy `
>   -SecretContentType "application/x-pkcs12" `
>   -SubjectName "CN=contoso.com" `
>   -IssuerName "Self" `
>   -ValidityInMonths 12 `
>   -ReuseKeyOnRenewal
> ```
>
> 2-
>
> ```powershell
> Add-AzKeyVaultCertificate -VaultName "ContosoKeyVault" `
>   -Name "ContosoDevCert" `
>   -CertificatePolicy $certificatepolicy
> ```

---

## ⁉️ Q40

You are planning to use Azure Functions to build an app that handles non-HTTP triggers. However, the language you want to use is not supported natively by Azure Functions. You decide to write a custom handler and ensure that your custom handler can handle processing requests within 90 seconds of function invocation.

Will this approach meet the execution requirements of Azure Functions?

---

> 👉🏻 **Explanation**
>
> **✅ the answer:**
> No — it will not meet the requirement. A custom handler must respond to the Functions host within **60 seconds** of invocation; 90 seconds is too slow.
>
> **🤔 Why This Is the Best Answer:**
> Azure Functions custom handlers have a host–handler handshake timeout: when any trigger fires, the Functions host sends an HTTP request to your custom handler and expects a response **within 60s**. If the handler doesn’t respond in that window, the invocation is marked failed, regardless of the broader execution limits of your plan.
>
> **❌ Why Other Options Are Wrong:**
>
> - “Yes, because Consumption allows 5–10 minutes.” → That’s the **overall function timeout**, not the **custom-handler response window**; the 60s handshake still applies.
> - “Yes on Premium/Dedicated (unlimited).” → Plan limits don’t override the 60s custom-handler response requirement.
> - “Only HTTP triggers have a short timeout.” → Even for non-HTTP triggers, the host calls the custom handler over HTTP internally, so the 60s response rule still applies.

---

## ⁉️ Q36

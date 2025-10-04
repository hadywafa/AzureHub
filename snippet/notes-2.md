# 📒 **Notes 1**

## Questions 1

> 🚨 Note:  
> 🔹 If you're planning a lift-and-shift migration, consider Azure Files to minimize code changes while enjoying cloud benefits.

## 💡 Quick Memory Tip

> 🚨 Note:  
> 🔹 CORS is only relevant when a **browser-based client app** (JavaScript in browser) tries to call your API/function from another domain.  
> 🔹 If you configure `AllowedOrigins = internal IP`
>
> - ❌ this doesn’t actually make sense because CORS doesn’t check **IP addresses**; it checks the **domain/origin header** (`https://example.com`). So the “IP” option is misleading/wrong.
>
> ---
>
> 👉🏻 If your API is **only server-to-server (Azure service → Azure service)** → set **CORS = none**.  
> 👉🏻 If your API is **called by a browser client (like React/Angular app)** → configure `AllowedOrigins` to **specific trusted domains only**.

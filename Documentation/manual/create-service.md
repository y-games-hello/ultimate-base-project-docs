# 🛠 How to Create a Service in UBP

This guide explains how to create your own UBP service, either:
- **Without configuration** — simplest path
- **With configuration** — editable via UBP Settings Window

> ⚠️ **Important:** All services are automatically discovered and registered when the game starts.

---

## 1️⃣ Create a Basic (Configless) Service

If your service doesn’t need any editable settings:

```csharp
using System.Threading.Tasks;

public class SampleService : IService
{
    public SampleService() { } // Parameterless constructor required

    public Task InitializeAsync()
    {
        // Initialization logic here
        return Task.CompletedTask;
    }
}
```

✅ That’s it — the framework will automatically create, register and inject dependencies for this service.

---

## 2️⃣ Create a Configured Service (with UBP Settings support)

If you want your service to have editable settings in the **UBP Settings Window**:

### Step 2.1 — Create the config ScriptableObject

```csharp
using UnityEngine;

[CreateAssetMenu(fileName = nameof(SampleServiceConfig), menuName = "Configs/Services/" + nameof(SampleServiceConfig))]
public class SampleServiceConfig : ScriptableObject
{
    [field: SerializeField] public string ExampleSetting { get; private set; } = "Default value";
}
```
This asset will hold all editable settings for your service.

---

### Step 2.2 — Create the service class

```csharp
using System.Threading.Tasks;

public class SampleService : ConfiguredService<SampleServiceConfig>
{
    public SampleService() { } // Parameterless constructor required

    // Returns the active config instance for this service
    public override SampleServiceConfig ServiceConfig =>
        ConfigStorage.GetConfig<SampleServiceConfig>();

    public override Task InitializeAsync()
    {
        // Use ServiceConfig.ExampleSetting here
        return Task.CompletedTask;
    }
}
```
Inheriting from `ConfiguredService<TConfig>` requires from you to implement ServiceConfig property, which returns the active configuration instance for this service.

---

## 🏆 Best Practices
- `InitializeAsync()` is called after creation — do all setup work here
- Do **not** put heavy logic in the constructor

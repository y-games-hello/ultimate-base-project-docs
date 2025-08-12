# ⏱ Updater Service

The **UpdaterService** allows plain C# objects to hook into Unity’s `Update`, `FixedUpdate`, and `LateUpdate` loops without inheriting from `MonoBehaviour`.

It manages object registration and ensures update callbacks are delivered efficiently through an internal `Updater` component.

---

## ✅ Features

- Allows you register/unregister objects for:
  - **`Update()`** (per frame)
  - **`FixedUpdate()`** (fixed timestep, physics-safe)
  - **`LateUpdate()`** (end-of-frame logic)
- Safely handles null objects and delayed registration/unregistration
- Works seamlessly across all scenes

---

## 🧪 Example Usage

Register an object that implements update interfaces:

```csharp
public class PlayerController : IUpdatable, IFixedUpdatable
{
    public void Update()
    {
        // Frame-based logic
    }

    public void FixedUpdate()
    {
        // Physics-based logic
    }
}
```

Register this way:
```csharp
Services.Get<UpdaterService>().Register(playerController);
```
Or through the `FactoryService`:
```csharp
Services.Get<FactoryService>().InjectDependency(playerController);
```
---
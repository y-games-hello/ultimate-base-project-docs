# ⏱ Updater Service

The **UpdaterService** allows plain C# objects to hook into Unity’s `Update`, `FixedUpdate`, and `LateUpdate` loops without inheriting from `MonoBehaviour`.

It manages object registration and ensures update callbacks are delivered efficiently through an internal `Updater` component.

---

## 🔧 What It Does

- Lets you register/unregister objects for:
  - **`Update()`** (per frame)
  - **`FixedUpdate()`** (fixed timestep, physics-safe)
  - **`LateUpdate()`** (end-of-frame logic)
- Safely handles null objects and delayed registration/unregistration

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

// Somewhere in initialization:
Services.Get<UpdaterService>().Register(playerController);
```

Unregister when done:

```csharp
Services.Get<UpdaterService>().Unregister(playerController);
```

---

## 🔄 Integration with Other Services

The `UpdaterService` is often used alongside the **FactoryService**'s `UpdaterPostProcessor`, which automatically registers any object implementing:

- `IUpdatable`
- `IFixedUpdatable`
- `ILateUpdatable`

This means your services and systems can start receiving Unity update events without any manual registration code.

---

## ✅ Use Cases

- Update loops for services or managers
- Game systems that run outside MonoBehaviours
- Physics-based calculations in non-MonoBehaviour classes
- Late-frame logic (e.g., camera adjustments, post-processing triggers)

This service helps decouple update logic from Unity components, making your architecture more modular and testable.

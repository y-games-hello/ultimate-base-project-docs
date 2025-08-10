# 🏭 Factory Service

The **FactoryService** is responsible for applying dependency injection or post-construction logic to objects using dynamically discovered `IPostProcessor` implementations.

This allows you to extend behavior without hardcoding dependencies, making your architecture clean and decoupled.

---

## 🔧 What It Does

- Scans all assemblies for classes that implement `IPostProcessor`
- Instantiates and stores all valid processors at runtime
- Allows you to call `InjectDependency(object)` on any object to trigger all processors

---

## 🧪 Example Usage

Inject dependencies or trigger setup logic on an object:

```csharp
Services.Get<FactoryService>().InjectDependency(myObject);
```

This will run **all registered processors** on `myObject`.

---

## 🔄 Integration with Other Services

FactoryService comes with a built-in processor:

### `UpdaterPostProcessor`

Automatically registers any object that implements:

- `IUpdatable`
- `IFixedUpdatable`
- `ILateUpdatable`

into the `UpdaterService`, allowing plain C# objects to receive Unity update events.

---

# 🧩 Creating a Custom PostProcessor

The `FactoryService` automatically applies logic to objects after creation using a system of pluggable **PostProcessors**. These are ideal for injecting dependencies, registering objects to other services, or setting up runtime logic.

This guide explains how to implement and register your own `IPostProcessor`.

---

## 1. Create a Class that Implements `IPostProcessor`

Your custom processor must implement the `Process(object target)` method.

### Example:
```csharp
using UBP.Scripts.UBPServices.Factory.PostProcessors;

public class SamplePostProcessor : IPostProcessor
{
    public void Process(object target)
    {
        if (target is SampleClass sampleObject)
        {
            //Do something with sampleObject
        }
    }
}
```

---

## 2. No Manual Registration Required

All post processors are automatically discovered at runtime, as long as:

- They implement `IPostProcessor`
- Are non-abstract
- Have a public parameterless constructor

> ✅ You do NOT need to manually register them.

---

## 3. Injecting Dependencies into Your Objects

To apply your custom logic to an object:

```csharp
Services.Get<FactoryService>().InjectDependency(myObject);
```

This will run your `Process()` logic along with all other registered processors.

---

## ✅ Use Cases

- Inject services into plain C# objects
- Register objects to update services
- Auto-bind event handlers
- Apply configuration data

This system helps decouple your architecture and removes boilerplate setup code.

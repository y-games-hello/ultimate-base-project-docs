# 🏭 Factory Service

The **FactoryService** is responsible for applying dependency injection or post-construction logic to objects using dynamically discovered `IPostProcessor` implementations.

This allows you to extend behavior without hardcoding dependencies, making your architecture clean and decoupled.

---

## ✅ Features

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

## 🛠️ How To Create Custom Post Processor

The `FactoryService` applies logic to objects using a system of pluggable **PostProcessors**. These are ideal for injecting dependencies, handling interfaces, registering objects to other services, or setting up runtime logic.

---

### 1. Create a Class that Implements `IPostProcessor`

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

### 2. No Manual Registration Required

All post processors are automatically discovered at runtime, as long as:

- They implement `IPostProcessor`
- Are non-abstract
- Have a public parameterless constructor

---

### 3. Injecting Dependencies into Your Objects

To run injection process on the object call:

```csharp
Services.Get<FactoryService>().InjectDependency(myObject);
```

This will run your `Process()` logic along with all other registered processors.

---

## 🏆 Best Practices
- Decouple your architecture by implementing more interfaces
- 

# 📦 Application Events Service

The **Application Events Service** provides a centralized, non-MonoBehaviour way to react to Unity’s core lifecycle events — such as **pause**, **focus**, **quit**, and **destroy** — from any part of your codebase.

This is particularly useful when you want backend systems (services, managers, etc.) to respond to application-level events **without needing a MonoBehaviour**.

---

## ✅ Features

- Listen to **OnApplicationPause**, **OnApplicationFocus**, **OnApplicationQuit**, and **OnDestroy** from any system.
- Events are forwarded through a persistent dispatcher object.
- Works across all scenes — no need to add MonoBehaviours manually.

---

## 🧪 Example Usage

```csharp
public class SampleClass
{
    public SampleClass()
    {
        var appEvents = Services.Get<ApplicationEventsService>();
        
        appEvents.OnApplicationPause += paused => Debug.Log($"Paused: {paused}");
        appEvents.OnApplicationFocus += focused => Debug.Log($"Focused: {focused}");
        appEvents.OnApplicationQuit += () => Debug.Log("Application is quitting");
        appEvents.OnApplicationDestroy += () => Debug.Log("App destroy lifecycle event");
    }
}
```

---

## 🔄 Event Reference

| Event                    | Description |
|--------------------------|-------------|
| `OnApplicationPause`     | Invoked when the application is paused or resumed. |
| `OnApplicationFocus`     | Invoked when the application gains or loses focus. |
| `OnApplicationQuit`      | Invoked right before the application quits. |
| `OnApplicationDestroy`   | Invoked when the dispatcher GameObject is destroyed. |

---

## 🧱 Internal Structure

### ApplicationEventsService.cs

- A pure C# class implementing `IService`
- Exposes `Action` delegates for Unity lifecycle hooks
- Instantiates a dispatcher GameObject and makes it persistent

### ApplicationEventsDispatcher.cs

- A hidden MonoBehaviour attached at runtime
- Listens to Unity lifecycle events and routes them to the service
- Never needs to be manually placed in scenes

---

## 🧼 Best Practices

- Use this service when you want to react to app-level events from systems that don't derive from `MonoBehaviour`.
- In case when you want to handle these events from single and centralized place.

---
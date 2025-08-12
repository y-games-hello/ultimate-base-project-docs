# 🎭 Scenes Service

The **Scenes Service** is responsible for managing scene loading, unloading, and transitions in a structured and extensible way.  
It centralizes scene management, allowing for asynchronous loading, additive scenes, and event-driven scene lifecycle handling.

---

## ✅ Features

- **Async/sync scene loading** with callbacks
- **Additive scene loading** for multi-scene workflows
- **Events** for scene load/unload lifecycle
- A clean API for developers to load/unload scenes without directly interacting with `UnityEngine.SceneManagement`

---

## 🧪 Example Usage

Load a Scene:
```csharp
Services.Get<ScenesService>().LoadScene("GameScene");
```
Load a Scene Async:
```csharp
Services.Get<SceneService>().LoadSceneAsync("GameScene", progressCallback, completionCallback,
    allowSceneActivation: true, LoadSceneMode.Additive);
```

Unload a Scene Async:
```csharp
await Services.Get<ScenesService>().UnloadSceneAsync("GameScene");
```
---

## ⚙️ Configuration

Scene Service Config available in [UBP Settings Window](../ubp-settings-window.md):

```
Window > YGames > Ultimate Base Project > Scene Service
```

| Field               | Description                                                                                         |
|---------------------|-----------------------------------------------------------------------------------------------------|
| `GameIntroScene`   | The scene which UBP loads after EntryScene once all Services and Configs are loaded and initialized |
---
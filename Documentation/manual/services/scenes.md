# 🎭 Scenes Service

The **Scenes Service** is responsible for managing scene loading, unloading, and transitions in a structured and extensible way.  
It centralizes scene management, allowing for asynchronous loading, additive scenes, and event-driven scene lifecycle handling.

---

## Overview

The Scenes Service provides:
- **Asynchronous scene loading** with callbacks.
- **Additive scene loading** for multi-scene workflows.
- **Events** for scene load/unload lifecycle.
- A clean API for developers to load/unload scenes without directly interacting with `UnityEngine.SceneManagement`.

---

## Basic Usage

### Loading a Scene
```csharp
Services.Get<ScenesService>().LoadSceneAsync("GameScene");
```

### Loading a Scene Additively
```csharp
Services.Get<ScenesService>().LoadSceneAdditiveAsync("UIOverlay");
```

### Unloading a Scene
```csharp
Services.Get<ScenesService>().UnloadSceneAsync("UIOverlay");
```

---

## Example: Switching Scenes with a Transition
```csharp
async void SwitchToGameplay()
{
    await Services.Get<ScenesService>().LoadSceneAsync("GameplayScene");
}
```

---

## Events

The Scenes Service exposes events you can subscribe to:

```csharp
Services.Get<ScenesService>().SceneLoaded += sceneName =>
{
    Debug.Log($"Scene {sceneName} loaded successfully!");
};

Services.Get<ScenesService>().SceneUnloaded += sceneName =>
{
    Debug.Log($"Scene {sceneName} unloaded.");
};
```

---
# Getting Started

## ✅ Requirements
- Unity 2021.3 or newer

## 🚀 Quick Start

Follow these steps to get the **Ultimate Base Project (UBP)** up and running in just a few minutes.

---

### 1. Import the Asset

Import **Ultimate Base Project (UBP)** from the Package Manager into your Unity project.

---

### 2. Create the "Entry" Scene

Create a new empty scene and name it:

```
Entry
```

This scene will act as the bootstrapper — it's where all UBP services and configurations are initialized **before** your actual game begins.

---

### 3. Add the Entry Scene to Build Settings

- Go to `File > Build Settings`
- Click **"Add Open Scenes"** to include the current `Entry` scene
- Make sure it’s the **first** scene in the list (index `0`)

---

### 4. Open the UBP Settings Window

Navigate to:

```
Window > YGames > Ultimate Base Project
```

This opens the centralized UBP configuration window.

---

### 5. Set Your Game's Intro Scene

- In the UBP Settings window, select the **Scene Service** tab
- Set the **"Game Intro Scene"** field to the name of your first real gameplay scene (e.g. `MainMenu`, `Gameplay`, etc.)
- UBP will automatically load this scene after initializing all services and configuration

---

### 6. Start Using UBP Services

Once the Entry scene initializes UBP, you can immediately call core services from anywhere in your code:

```csharp
Audio.Play("ButtonClick");
SaveSystem.Save();
Scenes.Load("Level2");
```

---

You’re now ready to build your game on top of a solid, service-driven foundation 🚀

## 🧩 Service-Based Architecture

UBP is built around a **modular service system**. Every major system (Audio, Save, Scenes, etc.) is managed as a service and accessible from anywhere in the project.

You can access services directly from the **Services Locator**.

### Example: Custom Access via Locator
```csharp
Services.Get<SaveService>().SaveGame();
```

You can also define and register your own services easily. See [Create Service](./create-service.md) for more info.

---
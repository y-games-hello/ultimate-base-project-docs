# Getting Started

## ✅ Requirements
- Unity 2021.3 or newer
---

## 🚀 Quick Start


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
- Click **"Add Open Scenes"** to include the currently opened `Entry` scene or drag it into the list
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
- Set the `GameIntroScene` field to the first real gameplay scene (e.g. `MainMenu`, `Gameplay`, etc.)
- UBP will automatically load this scene after initializing all services

---

### 6. Start Using UBP Services

Once the Entry scene initializes UBP, you can immediately call all services from anywhere in your code:

```csharp
Services.Get<AudioService>().Play("ButtonClick");
Services.Get<SaveService>().Save("playerData", playerData);
Services.Get<ScenesService>().LoadScene("GameScene");
```
---

You’re now ready to build your game on top of a solid, service-driven foundation.

You can also define and register your own services easily. See [Create Service](./create-service.md) for more info.

---
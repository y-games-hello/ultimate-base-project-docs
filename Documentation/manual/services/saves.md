# 💾 Save Service

The **SaveService** provides persistent data storage for your game, handling serialization, backup recovery, and both async and sync file operations.

This ensures safe and robust save/load functionality with minimal setup and full extensibility.

---

## ✅ Features

- Serializes and saves any object to disk (sync or async)
- Creates backups and handles recovery if the main save is corrupted
- Supports plug-and-play serializers (e.g., JSON, Binary)
- Automatically stores files under a configurable root folder

---

## 🧪 Example Usage

Save an object:

```csharp
Services.Get<SaveService>().Save("playerData", playerData);
```

Load it back:

```csharp
var data = Services.Get<SaveService>().Load<PlayerData>("playerData");
```

Or use async:

```csharp
await Services.Get<SaveService>().SaveAsync("playerData", playerData);
var data = await Services.Get<SaveService>().LoadAsync<PlayerData>("playerData");
```

---

## ⚙️ Configuration

Save Service Config available in [UBP Settings Window](../ubp-settings-window.md):

```
Window > YGames > Ultimate Base Project > Save Service
```

| Field               | Description                     |
|---------------------|---------------------------------|
| `SavesRootFolder`   | Root folder of all game saves   |
| `Open Saves Folder` | Opens the root saves folder     |
---

## 🔄 Save File Serializer

The `SaveService` uses a `SaveSerializer` to convert objects into a string format. By default, it uses:

### `JSONSaveSerializer`

This serializer wraps Unity’s built-in `JsonUtility` for fast and simple JSON serialization.

You can implement your own by inheriting `SaveSerializer` and overriding:

- `string Serialize<T>(T data)`
- `T Deserialize<T>(string data)`

Then assign your serializer during `SaveService` initialization:

```csharp
public class SaveService : ConfiguredService<SaveServiceConfig>{

    public override Task InitializeAsync()
    {
        _saveSerializer = new CustomSaveSerializer();
        return Task.CompletedTask;
    }
}
```

---

## 🏆 Best Practices

- Plug in custom serializers (JSON, binary, encrypted)
- Use async save/load for runtime stability
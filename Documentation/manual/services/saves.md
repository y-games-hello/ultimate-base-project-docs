# 💾 Save Service

The **SaveService** provides persistent data storage for your game, handling serialization, backup recovery, and both async and sync file operations.

This ensures safe and robust save/load functionality with minimal setup and full extensibility.

---

## 🔧 What It Does

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

## 🔄 Integration with Other Services

The `SaveService` uses a `SaveSerializer` to convert objects into a string format. By default, it uses:

### `JSONSaveSerializer`

This serializer wraps Unity’s built-in `JsonUtility` for fast and simple JSON serialization.

You can implement your own by extending `SaveSerializer` and overriding:

- `string Serialize<T>(T data)`
- `T Deserialize<T>(string data)`

Then assign your serializer in the `SaveService`.

```csharp
public override Task InitializeAsync()
{
    _saveSerializer = new JSONSaveSerializer();
    return Task.CompletedTask;
}
```

---

# ⚙️ Configuration

You can configure where save files are stored using:

### `SaveServiceConfig`

Located in your project under:

```
Configs/Services/SaveServiceConfig.asset
```

#### Example:
```csharp
[field: SerializeField] public string SavesRootFolder { get; private set; } = "Saves/";
```

All saves are stored inside:
```
Application.persistentDataPath + /SavesRootFolder/
```

---

# 🛡️ Backup & Recovery

If the original is corrupted, `SaveService` automatically attempts to load the **.bak** backup.

---

## 📁 File Structure

For a save called `"playerData"`, the following files are managed:

| Type      | File Path                            |
|-----------|--------------------------------------|
| Original  | `.../playerData.save`                |
| Temp      | `.../playerData.save.tmp`            |
| Backup    | `.../playerData.save.bak`            |

This structure provides automatic fallback and prevents permanent data loss.

---

## ✅ Use Cases

- Save/load game state, player data, or settings
- Plug in custom serializers (JSON, binary, encrypted)
- Auto-recover from corrupted saves
- Async save/load for runtime stability

The service helps you persist game data safely without writing redundant file or serialization logic.

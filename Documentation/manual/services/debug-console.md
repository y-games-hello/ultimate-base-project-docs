# 🐞 Debug Service

The **Debug Service** provides powerful runtime debugging tools. It captures logs, manages an in-game console, and supports registration of custom console commands.

---

## ✅ Features

- Captures **Unity log messages**
- Stores logs in a **bounded queue**
- Displays logs in a **persistent in-game console UI**
- Registers and executes **custom console commands**
- Toggleable with a keybind (e.g. `~`)
- Persists console window position and size across sessions

---

# 🛠️ Creating and Using a Custom Console Command

The in-game debug console allows you to register and run your own commands for testing, debugging, or cheat functionality.

Follow these steps to add a custom command to the console:

---

## 1. Create a New Command Class

Create a new class that inherits from `ConsoleCommand` and implement the `Execute` and `Undo` methods.

```csharp
using System;
using UnityEngine;
using UBP.Scripts.UBPServices.Debugs.ConsoleCommands;

public class PrintNameCommand : ConsoleCommand
{
    public PrintNameCommand(Type[] requiredArguments) : base(requiredArguments) {}

    public override void Execute(object[] arguments)
    {
        var name = arguments[0] as string;
        Debug.Log($"Hello, {name}!");
    }

    public override void Undo() { }
}
```

- The constructor defines what argument types are required.
- The `Name` is automatically taken from the class name (`PrintNameCommand`).
- The `Execute` method receives user input as `object[]`.

---

## 2. Register the Command in Code

Register your command so the console can recognize it:

```csharp
Services.Get<DebugService>().RegisterCommand(new PrintNameCommand(new[] { typeof(string) }));
```

Place this call during initialization (e.g. in a MonoBehaviour's `Start()` or a service setup phase).

---

## 3. Execute the Command from the Console UI

- Enter Play Mode and open the debug console (default: `~` key).
- Type your command using the expected arguments:

```
PrintNameCommand John
```

You should see this in the Unity Console:

```
Hello, John!
```

---

## 💡 Notes

- Only active in **development builds** (`Debug.isDebugBuild`)
- The command system automatically checks the number and type of arguments.
- You can define any number of parameters using different types (`int`, `bool`, `float`, etc.).
- `Undo()` is optional and can be left empty if not needed.

This system is ideal for:

- Enabling cheat/debug tools
- Quickly simulating gameplay events
- Testing systems without building UI

## ⚙️ Configuration
```
Window > YGames > Ultimate Base Project > Debug Service
```

| Field | Description |
|---|---|
| `MaxLogMessagesCapacity` | Max number of logs to store in memory |
| `ConsoleCanvasPrefab` | Prefab shown when toggling console |
| `OpenConsoleKey` | KeyCode to toggle the console |
| `LogMessageColor` | Log message color |
| `WarningMessageColor` | Warning message color |
| `ErrorMessageColor` | Error message color |
---
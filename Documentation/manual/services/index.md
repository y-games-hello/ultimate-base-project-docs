# Services

UBP Services provide a modular, scalable way to add functionality to your Unity projects. Each service is designed to handle a specific system or feature—such as saving data, managing update loops, or handling scene transitions—allowing you to keep your code clean and maintainable.

### All available services:

- [SaveService](saves.md)  
  Handles saving and loading game data safely and asynchronously with backup support.

- [UpdaterService](updater.md)  
  Provides custom update loops for non-MonoBehaviour objects, supporting Update, FixedUpdate, and LateUpdate callbacks.

- [SceneService](scenes.md)  
  Manages scene loading and unloading, including async operations and scene lifecycle events.

- [AudioService](audio.md)  
  Manages all audio playback and settings across the project.

- [ApplicationEventsService](application-events.md)  
  Provides centralized event hooks for Unity application lifecycle events like focus changes, pauses, and application exit.

- [DebugService](debug-console.md)  
  An in-game console for viewing logs and executing commands at runtime.

- [FactoryService](factory.md)  
  Responsible for applying dependency injection or post-construction logic.

---
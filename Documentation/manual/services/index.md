# Services

Welcome to the UBP Services documentation!  
UBP Services provide a modular, scalable way to add functionality to your Unity projects. Each service is designed to handle a specific system or feature—such as saving data, managing update loops, or handling scene transitions—allowing you to keep your code clean and maintainable.

Below is a list of all available services with links to their detailed documentation pages:

## Services

- [SaveService](saves.md)  
  Handles saving and loading game data safely and asynchronously with backup support.

- [UpdaterService](updater.md)  
  Provides custom update loops for non-MonoBehaviour objects, supporting Update, FixedUpdate, and LateUpdate callbacks.

- [SceneService](scenes.md)  
  Manages scene loading and unloading, including async operations and scene lifecycle events.

- [AudioService](audio.md)  
  Manages all audio playback and settings across the project. Supports volume control, audio groups, spatial audio, and global audio management.

- [ApplicationEventsService](application-events.md)  
  Provides centralized event hooks for Unity application lifecycle events like focus changes, pauses, and application exit, enabling modular response handling.

- [DebugService](debug-console.md)  
  An in-game console for viewing logs and executing commands at runtime. Improves debugging and testing with runtime log display and input capabilities.

- [FactoryService](factory.md)  
  Responsible for applying dependency injection or post-construction logic to objects using dynamically discovered `IPostProcessor` implementations.

---

Explore each service page to learn how to integrate, configure, and extend the services to fit your project's needs.

# 🔊 Audio Service

The **Audio Service** provides a centralized, pooled system for playing **sound effects (SFX)** and **music** across your game. It supports volume control through Unity’s built-in **AudioMixer**, and handles audio source reuse to avoid unnecessary allocations and runtime overhead.

---

## ✅ Features

- Plays **2D/3D sound effects**
- Plays **Music and SFX** with volume and pitch control
- **Pooled AudioSources** for optimized performance
- Volume control for **SFX** and **Music** via `AudioMixerGroup`
- Works seamlessly across all scenes

---

## 🧪 Example Usage

### Play a Sound Effect (SFX)

```csharp
Services.Get<AudioService>().PlaySFX(sfxClip, transform.position);
```

With custom volume and pitch:

```csharp
Services.Get<AudioService>().PlaySFX(sfxClip, transform.position, volume: 0.8f, pitch: 1.2f);
```

---

### Play Music

```csharp
Services.Get<AudioService>().PlayMusic(musicClip);
```

With custom volume, pitch, and loop settings:

```csharp
Services.Get<AudioService>().PlayMusic(musicClip, volume: 0.5f, pitch: 1f, loop: true);
```

---

### Set SFX or Music Volume (0 to 1)

```csharp
Services.Get<AudioService>().SetSFXVolume(0.7f);
Services.Get<AudioService>().SetMusicVolume(0.3f);
```

---

## ⚙️ Configuration

The service uses a `ScriptableObject` for settings:

```csharp
[CreateAssetMenu(fileName = "AudioServiceConfig", menuName = "Configs/Services/AudioServiceConfig")]
public class AudioServiceConfig : ScriptableObject
{
    public int AudioSourcesPoolSize = 10;
    public AudioMixerGroup MusicAudioMixerGroup;
    public AudioMixerGroup SFXAudioMixerGroup;
}
```

Set these values via the **UBP Settings Window**:

```
Window > YGames > Ultimate Base Project > Audio Service
```

---

## 🎛️ Inspector Settings

| Field                     | Description                                      |
|---------------------------|--------------------------------------------------|
| `AudioSourcesPoolSize`    | Number of `AudioSources` pre-created at startup. |
| `MusicAudioMixerGroup`    | Mixer group used for music playback.             |
| `SFXAudioMixerGroup`      | Mixer group used for SFX playback.               |

Make sure your **Audio Mixer** has exposed volume parameters named `"Volume"` to allow runtime volume adjustments.

---
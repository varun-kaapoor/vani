# Vani — Private dictation for your Mac

**वाणी** (Hindi for *voice or speech*)

Hold ⌥ Option, speak, release — your words appear at the cursor in any app. No cloud. No subscription. Everything stays on your Mac.

![macOS 26](https://img.shields.io/badge/macOS-26%20Tahoe-black) ![Apple Silicon](https://img.shields.io/badge/Apple%20Silicon-required-orange) ![Free](https://img.shields.io/badge/price-free-green)

---

## What it does

Vani is a menubar dictation app for macOS. Hold a hotkey, speak naturally, release — your words are transcribed on-device and typed at your cursor. Works in any app: Mail, Slack, Notes, Notion, Terminal, anything.

- **100% on-device** — WhisperKit runs Whisper on Apple's Neural Engine
- **AI cleanup** — Apple Intelligence removes filler words and adds punctuation locally  
- **No cloud, no account, no subscription** — nothing leaves your Mac
- **Learns your vocabulary** — auto-recognises names, jargon, and technical terms over time

---

## Download

**[Download Vani →](https://github.com/varun-kaapoor/vani/releases/latest)**

Requires macOS 26 Tahoe · Apple Silicon (M1 or later) · ~150MB on first launch

---

## How it works

```
Hold ⌥ Option       →   Recording starts
Speak naturally     →   Whisper transcribes on Neural Engine  
Release             →   AI cleans up → text appears at cursor
```

Three ways to dictate:
| Hotkey | Mode |
|---|---|
| Hold ⌥ | Push-to-talk — release to stop |
| Double-tap ⌥ | Hands-free — tap again to stop |
| ⌥ + Space | Alternative hands-free trigger |

Hotkey is configurable (⌥ Option / ⌃ Control / ⌘ Command / Fn) in Settings.

---

## Pipeline

```
Hotkey released
  → AudioRecorder.stop()          WAV capture via AVAudioEngine
  → TranscriptionEngine            WhisperKit (openai_whisper-base, on-device)
  → CleanupEngine                  Apple Intelligence or Ollama (local)
  → PasteEngine                    CGEvent Cmd+V at cursor
  → VocabularyStore                SwiftData — learns from each dictation
```

---

## Privacy

| What | Where it goes |
|---|---|
| Your voice | Stays on device — processed by WhisperKit locally |
| Transcribed text | Stays on device — never sent anywhere |
| AI cleanup | Apple Intelligence runs locally on Neural Engine |
| Usage stats | Stored locally in UserDefaults — never transmitted |

No telemetry. No crash reporting. No API keys. No internet connection required after the initial model download.

---

## Installation

1. Download the DMG from [Releases](https://github.com/varun-kaapoor/vani/releases)
2. Drag **Vani** to your `/Applications` folder
3. Open Vani from Applications (not from the DMG)
4. Grant **Microphone** and **Accessibility** permissions when prompted
5. Wait ~1 minute on first launch for the Whisper model to download
6. Hold ⌥ Option anywhere and start dictating

---

## Help & Feedback

- **Help:** [varun-kaapoor.github.io/vani/help](https://varun-kaapoor.github.io/vani/help)
- **Feedback / bugs:** [varun-kaapoor.github.io/vani/feedback](https://varun-kaapoor.github.io/vani/feedback)

---

## Tech stack

| Layer | Technology |
|---|---|
| UI | SwiftUI + AppKit |
| Transcription | [WhisperKit](https://github.com/argmaxinc/WhisperKit) — `openai_whisper-base` |
| AI cleanup | Apple FoundationModels (`SystemLanguageModel`) |
| Persistence | SwiftData |
| Hotkeys | `NSEvent` global monitors |
| Paste | CGEvent + NSPasteboard |
| Auto-updates | [Sparkle](https://github.com/sparkle-project/Sparkle) |

---

Built by [Varun Kapoor](https://github.com/varun-kaapoor) · Free & open source

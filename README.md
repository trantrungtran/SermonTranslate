# SermonTranslate

iPhone app for live sermon translation with biblical accuracy — inspired by Transync AI’s real-time bilingual captions and voice playback, specialized for Christian worship contexts.

## Features

1. **Full sermon recording** — captures the entire service audio
2. **Full transcript** — streaming speech-to-text saved with the session
3. **From / to language selection** — 20+ languages for source and target
4. **Near-live translation** — segment-based pipeline that waits for sentence boundaries so accuracy stays high
5. **Near-live interpretation** — optional TTS voice playback of the translation
6. **Display modes** — both languages, original only, or translation only
7. **Transync-like UX** — one-way listening mode, dual/single panel, AI terminology assistant, session records, voice playback, PiP-ready subtitle settings
8. **Bible-aware translation** — detected scripture references use the exact verse text in the chosen Bible edition instead of machine-translating the quote
9. **No profanity** — filtered from transcripts and spoken output

## Requirements

- macOS with Xcode 16+
- iOS 17+ device or simulator
- Microphone + Speech Recognition permissions

## Open in Xcode

```bash
open SermonTranslate.xcodeproj
```

Select an iPhone simulator or device, then Run (⌘R).

## Architecture

| Layer | Role |
|-------|------|
| `Views/` | SwiftUI screens (live session, records, settings) |
| `Services/` | Recording, speech, translation, Bible lookup, TTS, profanity |
| `Models/` | Session, segments, languages, display modes |
| `Resources/` | Bundled Bible excerpts, Christian glossary, profanity list |

### Live pipeline (accuracy over raw latency)

1. Microphone → continuous speech recognition
2. On sentence/clause boundary → finalize segment
3. Detect Bible references → substitute exact verse text
4. Translate remaining text with Christian-context prompt
5. Apply profanity filter
6. Update bilingual UI + optional voice playback

## Bible editions

In Settings, choose the target-language Bible edition used when a verse is quoted (e.g. NIV, ESV, KJV, RVR1960, CUV). The app never paraphrases detected scripture; it inserts the official verse text for that edition when available.

## API keys (optional)

On-device Apple Speech works without keys. For higher-quality translation beyond Apple’s Translation framework, set `OPENAI_API_KEY` in the Xcode scheme environment, or enter it under Settings → Translation Provider.

## Privacy

Audio and transcripts stay on device by default. Optional cloud translation is only used when an API key is configured.

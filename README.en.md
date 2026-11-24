# Meeting Assistant

Listens, takes notes and can speak for you. Microphone and system loopback are recorded and transcribed on separate channels - cloud or fully local - and the AI advisor can join at any time based on the latest discussion. One click at the end produces a structured Markdown summary.

## What it does

- **Dual-channel recording** - microphone (your side) and system loopback (remote side) captured and transcribed separately, so speaker attribution is structural rather than guessed.
- **Cloud or local transcription** - choose a cloud STT endpoint, or a local whisper / FunASR engine installed by the Local ASR plugin; local mode never sends audio out.
- **Live captions and AI advisor** - the advisor reads the recent transcript and can be invited to speak at any moment.
- **Meeting summaries** - structured Markdown with decisions, action items and risks.
- **Audio files** - transcribe an existing recording afterwards.
- **Environment check** - validates ffmpeg, microphone and loopback devices, and transcription configuration before a meeting.

## Permissions and privacy

- `process`, `network`, local storage.
- Recordings and transcripts stay in the local `userData` directory. Network access happens only for a cloud STT or LLM endpoint you configured.

## Links

- Marketplace: https://ruodao.com/plugin-market

## License

MIT

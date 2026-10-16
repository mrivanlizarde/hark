# Hark

Turns any audio or video file on your Mac into a transcript with speaker labels:
who said what, not just what was said.

Everything runs on your Mac. No account, no API key, no subscription, no per-minute cost,
and nothing is uploaded. After a one-time model download it works offline.

```
Speaker 1: Hi, Daniel. Thanks for joining the call today.

Speaker 2: Happy to be here. I have a few questions about the report.
```

## Use

- **Drop a file on Hark.** The transcript lands next to it as a `.txt`, and you can name
  the speakers.
- **Or right-click any audio or video file in Finder** → Quick Actions → **Transcribe with
  Hark**.

## Install

Hark isn't notarized by Apple, so there's no download yet. You build it yourself in a few
minutes. You need **macOS 26 or later on Apple Silicon** and Apple's command line tools
(run `xcode-select --install` once if you've never built anything).

```sh
git clone https://github.com/mrivanlizarde/hark.git
cd hark
./make-app.sh release --install
./install-quick-action.sh
open ~/Applications/Hark.app
```

The first line builds Hark and puts it in your Applications folder. The second adds the
Finder right-click action. The first transcription downloads the speaker models once;
after that it works offline.

## Why macOS 26 and Apple Silicon

Both are hard requirements. Transcription uses Apple's `SpeechAnalyzer`, which doesn't exist
before macOS 26, and its speech models aren't available on Intel.

## How it works

Apple's `SpeechAnalyzer` transcribes with word-level timestamps. Apple's speech framework
can't tell speakers apart, so [FluidAudio](https://github.com/FluidInference/FluidAudio)
works out who is talking when. The two are merged on the timeline into speaker-labeled
blocks.

There's also a command-line version for scripting, with `txt`, `srt`, `vtt`, `markdown`
and `json` output. See [START_HERE.md](START_HERE.md).

## Tip jar

Hark is free and stays free. If it saved you an afternoon of typing, you can buy me a
coffee: [buymeacoffee.com/mrivanlizarde](https://buymeacoffee.com/mrivanlizarde).

## License

MIT. See [LICENSE](LICENSE). The speaker engine, FluidAudio, is Apache 2.0.

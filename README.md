# chillbook

**Turn an e-book into an audiobook, on your own computer.** Drop in an `.epub` or `.pdf`, pick the chapters and a voice, hear a sample from your own book, see what it will cost, and press Convert. You get one `.m4b` audiobook file, with a chapter marker for each chapter, the book's title, author and cover, and every chapter at the same loudness. Play it in any audiobook app.

The program is called **book2audio**. This repository, chillbook, is a fork of [Claudemy](https://github.com/assafkip/claudemy) by Assaf Kipnis (MIT) that adds it. The original Claudemy skill is still here, unchanged; see [Credits](#credits-and-licence).

## Two ways to use it

**A web page on your own computer** (easiest). Nothing is hosted: a small program opens a page in your browser, only your own computer can reach it, and nothing from your book leaves your computer unless you choose a cloud voice.

- Pick chapters from a list (copyright pages and indexes are left out for you, with the reason).
- Choose a voice and press ▶ **Sample** to hear it read the start of your own book. A paid sample shows its cost first.
- A summary shows the length of the audiobook, a rough time, the cost, and **where your text goes**.
- Stop at any time and carry on later: finished parts are never made (or paid for) twice.

**The command line**, for scripts and people who like a terminal: `book2audio mybook.epub --dry-run` lists chapters, size, time and cost and spends nothing; `book2audio mybook.epub` makes the audiobook.

## Voices

| Voice | Cost | Where your text goes |
|---|---|---|
| Piper (free), macOS built-in voices | free | stays on your computer |
| ElevenLabs | paid, by your plan | sent to ElevenLabs |
| Google Cloud Chirp 3 HD | paid, per character | sent to Google Cloud |
| Claude clean-up (optional) | paid | sent to Anthropic |

**Your text leaves your computer with the paid services.** Only use them for books you are allowed to send, and check the provider's terms. API keys are typed into the page and kept in memory only: never saved to a file.

## Get it running

You need Python 3.10 or newer and ffmpeg.

```bash
# Windows: winget install Gyan.FFmpeg     macOS: brew install ffmpeg
git clone https://github.com/gcazzola/chillbook && cd chillbook
pip install ./book2audio
book2audio ui                    # opens the page in your browser
```

Or double-click `book2audio/Start Book2Audio.bat` (Windows) or `book2audio/Start Book2Audio.command` (macOS).

**Windows without installing anything:** `book2audio/packaging/` builds one portable zip with its own Python and ffmpeg (an LGPL build): unzip it and double-click. It is not published as a download yet; [how to build it](book2audio/packaging/README.md).

Full install steps, every option, how the text is prepared, limits and tests: [book2audio/README.md](book2audio/README.md).

## Where it stands

Built and tested with fake voice engines and mocks (about 140 automated tests, using a public-domain book). Tried live so far: short Google Chirp 3 HD and ElevenLabs samples. Not yet tried live: Piper, a full paid chapter, the Claude clean-up, a clean Windows PC for the portable zip. English only for now.

## Credits and licence

MIT; see [LICENSE](LICENSE), which keeps Assaf Kipnis's copyright notice and adds this fork's.

book2audio started from [Claudemy](https://github.com/assafkip/claudemy), Assaf Kipnis's skill that turns a topic into short audio lessons: its ElevenLabs request style and its ffmpeg concat and loudness step were adapted, and both are marked in the code. Everything else in `book2audio/` is new. Claudemy itself is untouched in `skills/claudemy/`, and its original README is kept in [CLAUDEMY.md](CLAUDEMY.md). To get Claudemy as its author ships it, use [the original repository](https://github.com/assafkip/claudemy).

Libraries were chosen to keep this project MIT: the GPL and AGPL ones (Piper, `ebooklib`, PyMuPDF) are either run as a separate program or not used.

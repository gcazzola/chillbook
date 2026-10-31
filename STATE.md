# STATE: book2audio in the fork gcazzola/chillbook

Updated 2026-10-31. Rewrite this file at the end of a work block; do not append.

## Where things stand
- `book2audio` is done as a CLI and as a web page: `book2audio ui` (127.0.0.1 only, token and Host/Origin checks, keys in memory only, voice samples, live cost and privacy summary, convert/stop/resume, first-run checklist, "Install it for me" for Piper). Launchers: `book2audio/Start Book2Audio.bat` and `.command`.
- Portable Windows bundle: `book2audio/packaging/build_windows_bundle.py` (Python 3.13 embeddable, LGPL ffmpeg, pinned and hash-checked; Piper left out on purpose). Last zip is in `%LOCALAPPDATA%\Temp\b2a-bundle\out` (not in git).
- 142 tests pass (last run at `140b60b`; `f454905` only changed READMEs). Security review of the branch: nothing at confidence 8 or higher.
- Git: everything is pushed to the fork. `feat/book2audio-ui` is at `f454905`, 20 commits ahead of `main`, and holds all of the work. `main` still equals Assaf's Claudemy. No PR yet. Never open a PR on `assafkip/claudemy`: GitHub offers it by default (done once by mistake, closed).
- Root `README.md` is rewritten around book2audio; the original Claudemy README is kept in `CLAUDEMY.md`.
- Live checks by the user: Google Chirp 3 HD samples (14 voices) and one ElevenLabs sample returned audio. Not yet live: a full paid chapter, Piper (install button, voice download), the Claude pass, the bundle on a clean or work PC, macOS (`say` list, `.command`).

## Open work
- Open the PR `feat/book2audio-ui` into `main` inside `gcazzola/chillbook` (check the base repository says gcazzola/chillbook) so the new README shows on the front page.
- Fancy README (banner, UI screenshots or GIF, Mermaid diagram, privacy callout, badges, collapsible sections, social preview image): a new session is being prepared for it.
- Still says Claudemy: repo description and topics, `.github/social-preview.png`, `llms.txt`, `.claude-plugin/`, `docs/` site.
- Publish the zip as a Release only after a clean-PC test and a licence check (the licence reading so far is not legal advice).
- First real chapter test: `book2audio BOOK --backend google --chapters 1 --yes` (or `--backend elevenlabs`).

## Out of date or unconfirmed
- Cost and time numbers are estimates; no price is built in (`--price-per-1k`). Google's Chirp 3 HD price and free allowance are unconfirmed.
- Google API-key auth is only community-confirmed; the documented path is a gcloud access token. The page's Google "Ready" check counts a `gcloud` on the PATH, which does not mean signed in.
- ElevenLabs fallback voice ids other than Liam are from memory; the account's own list replaces them once a key is added.

## Fragile
- PDF handling was tuned on one synthetic PDF; real books may need tuning (columns, tables, small print low on a page).
- Windows: use the short-path venv `%LOCALAPPDATA%\Temp\b2a-venv`; ffmpeg is installed by winget but not on PATH in the agent shell; `gh` is unavailable.
- Sessions share this one checkout (another session committed on this branch once): run `git branch --show-current` before committing.

## Where to look
- Docs: `book2audio/README.md`, `book2audio/packaging/README.md`. Code: `book2audio/src/book2audio/` (`cli.py`, `pipeline.py`, `tts.py`, `estimate.py`, `ui.py`, `voices.py`, `web/`).
- Tests: `cd book2audio && python -m unittest discover -s tests`.
- Voice sample script: `book2audio/examples/chirp3_sample.py`.

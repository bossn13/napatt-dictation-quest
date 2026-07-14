# Dictation Power-HUD Word Catcher

Gesture-controlled English vocabulary quiz for P.4, built as a single static file (`v3.html`). No build step, no backend.

## Run locally

Camera APIs (`getUserMedia`) require `http(s)://` or `localhost` — opening the file directly via `file://` will not allow camera access (touch-only mode will still work).

```bash
cd apps/vocab-quiz-p4
python3 -m http.server 8000
```

Then open `http://localhost:8000/v3.html` in a browser (desktop Chrome/Safari for webcam testing, or iPad Safari over your local network for full device testing).

## Desktop webcam smoke test

- Pick a subject, click "เริ่มภารกิจด้วยกล้อง", allow camera access.
- Cyan hand skeleton + gold fingertip reticle should track a real hand; a red-gold flame effect should flicker above your head and disappear cleanly when your face leaves frame (hand tracking keeps working).
- The definition/question text overlays the center of the camera stage (not a separate header) — confirm it stays readable over the live video and never gets covered by the flame effect.
- Hover the gold fingertip circle over an answer button — a gold ring should fill over ~650ms before the answer registers; moving off the button early should reset the ring to empty.
- Hover-hold "ฟังคำศัพท์" and "ออก" the same way; confirm a completed selection is followed by a ~900ms cooldown before another can start.
- Deny camera permission (or block it in browser settings) and confirm the full quiz — subject select through the 10-question round to the Mission Complete screen — is playable by mouse/tap click alone.
- Play through a full round and confirm no Thai text ever appears on the quiz screen itself (subject-select and button-label Thai chrome outside the quiz screen is expected).
- Click "ออก" and confirm the browser's camera indicator turns off.

## Manual iPad Safari checklist (cannot be automated)

- [ ] Camera opens only after tapping "เริ่มภารกิจด้วยกล้อง" — no fullscreen native video takeover.
- [ ] Every button (subject, answers, listen, exit, replay, back) responds instantly to a tap.
- [ ] Hand-hover gesture works at arm's length using the front camera in normal room lighting.
- [ ] "ฟังคำศัพท์" produces audible speech on the very first use after starting a mission (validates the iOS speech-synthesis gesture-unlock warm-up).
- [ ] Rotating the iPad re-syncs the camera stage and button hit-testing without misalignment.
- [ ] No major slowdown or overheating over a full 10-question round with both hand and face tracking running.

## Notes

- Vocabulary source: `../../KB/Vocabulary/20260520-vocab-p4-term1.md` (5 of 6 subjects kept; "SGI (Technology)" dropped per user decision). Thai definitions were intentionally not copied into this file — only English word/part-of-speech/definition are embedded, so the quiz screen structurally cannot render Thai vocabulary content.
- Deployed at https://bossn13.github.io/napatt-dictation-quest/v3.html — a separate repo from this one, containing only this game (no `/KB` personal data), so the child's real name/school/teacher info is never exposed.

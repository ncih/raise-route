# Raise Route — presenter ops guide

## The two pages

1. **Attendees:** QR points at `index.html` (GitHub Pages root of this folder). Phones only need a browser.
2. **Seeing results live = open `presenter.html` in a second browser tab on the laptop.** That page IS the live view — full-screen it (F11 / ⌃⌘F). It polls Supabase every 4 seconds. Switch to that tab at the results slide (slide 53 cue in the run sheet), and peek at it after each checkpoint cue.

## Checkpoint structure (attendee side)

Register → **CP0** warm-up (raise size) → **CP1** your raise (instrument + rails multi-select) → **CP2** Malaysia perimeter self-test (4 questions → verdict) → **CP3** build readiness (weakest layers, up to 2) → **CP4** is launching a token worth it? (5 statements → verdict) → **Finale** Raise Route boarding card (save-as-image). Every step has a Back button — going back and re-answering overwrites the stored answer.

## Gating — you control the pace

- Attendees can't run ahead: any checkpoint beyond the one you've opened shows a **waiting screen** ("Nicholas will open this one — eyes up front 👆") that polls every 5s and unlocks itself.
- **Control strip at the top of `presenter.html`:** "Open next →" advances the gate by one; the **CP0–CP4 chips** jump the gate directly (including backwards, if you ever need to re-close).
- Start of session: gate should read **CP0** (only register + warm-up open). Cue each checkpoint verbally, then hit **Open next**.
- **Fail-open by design:** if an attendee's phone can't reach Supabase, the gate does NOT block them — they can keep answering (better than a stuck phone in the room).

## Live Q&A

- Attendees get a floating **"Ask a question"** button (visible once registered, on every step incl. the finale). Questions land in the **Q&A panel** (bottom-right of the grid) newest-first, with name + company.
- **Tap a question to mark it answered** (it dims; tap again to un-dim). The panel header counts *unanswered* questions.
- Press **Q** to blow the Q&A feed up full-screen for a dedicated Q&A moment.

## Keys

**0–4** focus one checkpoint panel full-screen (the reveal moment) · **Q** full-screen Q&A · **Esc** back to the grid.

## Data & export

- Supabase project `hhqlzcvwalwuxrrolevv`: `leads` (registrations, insert-only), `answers` (cp0–cp4 per device + a cp5 completion flag), `questions` (Q&A), `session_state` (the gate — single row).
- Export after the session: Supabase dashboard → Table Editor → `leads` / `answers` / `questions` → export CSV. A `cp5` row for a device = finished the full route.
- Multi-select answers (CP1 rails, CP3 layers) are stored as arrays and tallied per-option on the room map.

## Fallback ladder (if something looks wrong mid-session)

1. **Room map looks empty / frozen:** check the laptop's own Wi-Fi first — attendee writes are fire-and-forget and catch up on their own. Amber "Reconnecting…" self-heals; do nothing.
2. **Attendee phone offline:** their answers queue locally (tiny dot, top-right of their screen) and sync when back online. A reloaded phone resumes exactly where it was (localStorage).
3. **Gate won't budge on phones:** the waiting screen re-checks every 5s — worst case tell the room "give it five seconds". If Supabase itself is down, phones fail open and simply won't be blocked; pace the room verbally.
4. **Presenter page dead entirely:** attendees are unaffected (their flow still works and still saves). Run the reveal moments verbally, export the tables afterwards.
5. **Everything down:** attendees still complete the route on-device and can screenshot their boarding card — the leads are re-sent automatically whenever their phone reconnects, even after the session.

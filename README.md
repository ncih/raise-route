# Raise Route — presenter ops guide

1. **Attendees:** QR points at `index.html` (GitHub Pages root of this folder). Phones only need a browser — no app, no sign-up.
2. **You:** open `presenter.html` on the laptop, full-screen it (F11 / ⌃⌘F). It polls Supabase every 4 seconds.
3. Green pulsing dot top-right = live; amber "Reconnecting…" = network blip — it self-heals, do nothing.
4. Press **0–5** to blow one checkpoint up full-screen for the reveal moment; **Esc** returns to the 6-panel grid.
5. Cue each checkpoint verbally — attendee steps unlock as they finish the previous one, no time-gating.
6. Attendee phones never block on network: answers queue locally and sync when back online (tiny dot, top-right of their screen).
7. A reloaded attendee phone resumes exactly where it was (state is in localStorage).
8. Data lives in Supabase project `hhqlzcvwalwuxrrolevv`: `leads` (registrations, insert-only) and `answers` (cp0–cp5 per device).
9. Export after the session: Supabase dashboard → Table Editor → `leads` / `answers` → export CSV. cp5 rows with `complete: true` = finished the full route.
10. If the room map looks empty mid-session: check the laptop's own Wi-Fi first — attendee writes are fire-and-forget and will catch up.

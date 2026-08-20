# Learned

One line per session. What I built, what broke, what I now understand.
This becomes the interview narrative, so write it while it is still fresh.

## Week 1

- **20 Aug 2026** — Set up the toolchain: Node 24 LTS, npm 11, GitHub CLI, VS
  Code on PATH. Chose to run n8n via `npx` rather than Docker, to keep the first
  session about workflows instead of about container setup.

  20 Aug 2026 — Built my first n8n workflow: schedule trigger → HTTP request → GitHub issues API. Learned that nodes run once per item automatically. Downloaded the output instead of the workflow the first time — they're different buttons.

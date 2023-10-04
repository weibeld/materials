---
meta:
  created: 2023-06-03T02:55:10+02:00
  edited: 2023-06-03T02:55:10+02:00
data:
  title: Pragmatic techniques to get the most out of GitHub Copilot
  date: 2023-05-24
  speakers:
    - name: Burke Holland
      affiliation: Microsoft
    - name: Allison Weins
      affiliation: GitHub
  event: microsoft-build-2023
  recording: https://build.microsoft.com/en-US/sessions/7a726a0f-5433-46a4-a91d-7d427ffb5b30
---

- Supercharged code completion
- New feature: chat function (preview)
- Usage examples:
  - Auto-complete short function from either a comment or function name
  - Auto-complete CSS from comments (e.g. "adda thin border")
  - Debugging (find out the reason for errors)
- Strengths:
  - Leverage for patterns and stuff you easily forget
    - E.g. CSS, Cron
- Can take code snippets from other open files
  - Tip: if references to other files are needed, open these files
- Chat function:
  - Can highlight code and ask Copilot what it does
  - Works in VS Code
    - Is it available in Vim?
  - In VSCode there is a function "solve with Copilot"
- Tips:
  - Iterate multiple times with prompt until the desired result appears
Resources:
  - https://resources.github.com/copilot-demo/

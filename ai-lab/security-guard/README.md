# 🛡️ Security guard skill

**Problem.** Giving an AI agent real access (servers, databases, chat, tickets) means it handles secrets and reads text written by other people. I wanted both to be boring and safe.

**What I built.** A Claude Code skill that loads whenever anything touches secrets, access or exposure.

| Piece | What it does |
|---|---|
| **Secret store** | Every credential lives in an auto-locking macOS Keychain, reached only through [wrappers](../zero-password-agent-access/) |
| **Weekly Mac check** | Read-only: lock settings, folder permissions, transcript retention, stray plain-text copies. Prints OK / WARN / FIX, never a value |
| **Plain-text finder** | Finds files that still hold a known secret. Prints the file and a count, never the secret |
| **Breach check** | Are any of our passwords in public breach lists? Uses k-anonymity: only the first 5 characters of a hash leave the Mac |
| **Untrusted text** | Anything read from Slack, Jira or the web is treated as data, never instructions |
| **Threat model** | A written threat model and a checklist for what to do if something ever leaks |

**Rules:** report everything, change nothing without a yes. Adding a new secret happens in a separate terminal window Claude never sees.

**Built with:** Claude Code skill, Python, macOS Keychain, Have I Been Pwned range API.

[← AI Lab](../README.md)

# Security policy

## Reporting a vulnerability

Please do not open a public issue for a security problem.

- Report it privately through GitHub: **Security** tab → **Report a vulnerability**.
- Or email **support@postsnag.com** with "Security" in the subject.

Include what you found, how to reproduce it, and what an attacker could do with it. We aim to acknowledge reports within 3 business days.

## Scope

This repository holds the PostSnag plugin for Claude: skill instructions (Markdown), the plugin manifest and the address of the PostSnag server (`.mcp.json`). It contains no executable code, hooks or credentials.

In scope here:

- a change that would point the plugin at a server other than `https://api.postsnag.com/mcp`
- skill text that could make Claude leak data or act against the user's instructions
- anything secret committed to this repository

Problems with the PostSnag service itself (the API, sign-in, the dashboard or the Chrome extension) are welcome at the same addresses.

## How this repository is protected

- `main` only changes through a reviewed pull request; force-pushes and deletion are blocked.
- Every pull request runs the `validate` check: the plugin may contain only Markdown, JSON and PNG files, `.mcp.json` must name the production PostSnag server and nothing else, and Claude's plugin directory checks must pass.
- GitHub secret scanning and push protection are on.

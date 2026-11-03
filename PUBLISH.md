# Publish this skill to a new GitHub repo

1. **Create the repo** on GitHub (e.g. `austindixson/openclaw-better-ralph` or your org/name). Do not add a README or .gitignore (this repo already has them).

2. **Set the remote** (if not already set):
   ```bash
   git remote add origin https://github.com/YOUR_ORG/openclaw-better-ralph.git
   ```
   Or if you created a different repo name, use that URL.

3. **Push**:
   ```bash
   git push -u origin main
   ```

Done. The skill is in `skills/better-ralph/SKILL.md`. Users can clone the repo and copy that folder to `~/.openclaw/skills/` or their project’s `skills/`.


## Tick Hosting — Translation System (Basic Documentation)

Overview
- This repository holds translations for Tick Hosting (tickhosting.com), a Minecraft hosting service offering both free and paid plans.
- The translation files are simple JSON files: one file per language. They contain key/value pairs where keys are the translation identifiers and values are the translated strings.

Files
- `english.json` — English strings (source / reference).
- `german.json` — German translations.
- `italian.json` — Italian translations.
- `README.md` — This document: basic instructions on how to edit and contribute translations.

Translation key format
- Each JSON file is a flat or nested object of key/value pairs. Keys are the unique identifiers used by the application; values are the localized strings.
- Example (flat):
	- `"home.title": "Welcome to Tick Hosting"`
- Example (nested):
	- `"home": { "title": "Welcome to Tick Hosting", "subtitle": "Free & paid Minecraft hosting" }`

Basic rules and conventions
- Use the English file (`english.json`) as the canonical source for keys and meaning.
- Keep keys stable. When changing or removing keys, coordinate with devs or include a note in the PR.
- Preserve placeholders exactly (see Placeholder rules below).
- Keep punctuation and capitalization appropriate for the language.
- Avoid adding HTML or platform-specific markup unless the application expects it.

Placeholders and interpolation
- If English values contain placeholders (like `{0}`, `{user}`, `%s`, or similar), translators must keep the placeholder tokens and adapt word order when needed.
- Common placeholder patterns:
	- Positional: `{0}`, `{1}`
	- Named: `{username}`, `{count}`
- Example:
	- `english.json`: `"welcome": "Hello, {username}! You have {unread} unread messages."`
	- `italian.json`: `"welcome": "Ciao, {username}! Hai {unread} messaggi non letti."`
- Do not translate the placeholder names. Only translate surrounding text.

Formatting rules
- Use Unicode (UTF-8) encoding.
- Keep strings as plain text (no markup) unless a specific string is meant to include HTML or Markdown — that should be clearly indicated in the key name or comments.
- If a value must include quotes, escape them properly for JSON (use backslash).

Validation & testing locally
- Always validate JSON syntax before opening a PR.
- Quick JSON validation (PowerShell):
	```powershell
	Get-Content .\english.json -Raw | ConvertFrom-Json > $null
	if ($?) { Write-Host "Valid JSON" } else { Write-Host "Invalid JSON" }
	```
- Using Python (if installed):
	```powershell
	python -m json.tool english.json > $null
	```
- Search for missing keys by comparing `english.json` to other language files. A small script (Node/Python) can compare keys and show missing entries — ask if you want one added to the repo.

How to add or update a translation
1. Fork this repository to your GitHub account.
2. Clone your fork and create a new branch for your work, e.g., `i18n/italian-update-home`.
3. Open the appropriate language file (e.g., `italian.json`) and add/update translations based on `english.json`.
4. Keep the JSON structure and placeholders consistent.
5. Validate JSON locally (see Validation & testing).
6. Commit your changes with a clear commit message (see Contributing below).
7. Push your branch to your fork and open a Pull Request (PR) against this repository's main branch.

Contributing & PR workflow (fork + PR required)
- We accept translation contributions via forks and pull requests. Please do not push directly to the main repository.
- Steps to contribute:
	1. Fork the repository on GitHub.
	2. Create a feature branch in your fork (e.g., `i18n/add-spanish`).
	3. Make changes and run JSON validation locally.
	4. Commit with a clear, concise message.
	5. Push the branch to your fork.
	6. Open a Pull Request to this repository's `main` branch.
	7. In the PR description include a short summary of changed/added keys and any context reviewers may need.
	8. Wait for review. Maintainers may request fixes or clarifications before merging.

Branch naming and commit message suggestions
- Branch names (examples): `i18n/italian-update-home`, `i18n/add-spanish`, `i18n/fix-german-typo`.
- Commit message examples:
	- `i18n: add Italian translations for home and billing`
	- `i18n: fix typo in German strings`

PR checklist for translations
- Include which language file(s) you changed.
- List any keys intentionally left blank or that need context.
- Confirm you validated JSON syntax.
- If you added a new language file, mark it as WIP in the PR title if incomplete (e.g., `i18n: add spanish.json (WIP)`).

Edge cases & tips
- If a language needs multiple plural forms, prefer using the app’s established pluralization keys (ask devs if no pattern exists).
- Keep text concise where the UI has limited space (tooltips, buttons).
- Avoid literal line breaks unless the UI supports multi-line strings — prefer `\n` when necessary and supported.

Optional: Automated checks (recommended)
- Add a CI check to validate JSON and check for missing keys. Example checks:
	- JSON syntax validation for each file.
	- Key presence: ensure every key in `english.json` exists in all other locale files (may allow empty strings for not-yet-translated keys).
- I can help add a small validation script or a GitHub Actions workflow if you want.

Contact / support
- If you are unsure about meaning or where a string appears in the UI, open an issue describing the key and request context/screenshots.
- For urgent translation fixes, mention the relevant dev in the PR or the project's communication channel.

Small examples
- `english.json`:
	```json
	{
		"home": {
			"title": "Welcome to Tick Hosting",
			"subtitle": "Free & paid Minecraft hosting"
		},
		"account": {
			"greeting": "Hello, {username}"
		}
	}
	```
- `italian.json`:
	```json
	{
		"home": {
			"title": "Benvenuto su Tick Hosting",
			"subtitle": "Hosting Minecraft gratuito e a pagamento"
		},
		"account": {
			"greeting": "Ciao, {username}"
		}
	}
	```

Wrap-up / Next steps
- This README now explains the translation system and the required fork + PR contribution flow.
- If you want, I can also:
	- Add a small JSON validation script to the repo.
	- Add a GitHub Actions workflow to validate locale files on PRs.
	- Create an issue template or PR template for translations.

If you'd like me to make one of those follow-ups, tell me which one and I'll add it next.

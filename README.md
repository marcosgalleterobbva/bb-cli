# bbdc-cli

A small, practical **Typer** CLI for **Bitbucket Data Center / Server** REST API.

It reads credentials from environment variables and gives you a few high-signal commands (list PRs, create PRs, comment, etc.) without needing a full SDK.

---

## Requirements

- Python 3.9+
- `pipx` recommended for isolated install

---

## Install (pipx)

From the project root (the folder containing `pyproject.toml`):

```bash
pipx install .

If you’re iterating on the code locally:

pipx install -e .

Reinstall after changes (non-editable install):

pipx reinstall bbdc-cli

Uninstall:

pipx uninstall bbdc-cli


⸻

Configuration

The CLI uses two environment variables:
	•	BITBUCKET_SERVER: base REST URL ending in /rest
	•	Example (BBVA-style context path):
https://bitbucket.globaldevtools.bbva.com/bitbucket/rest
	•	BITBUCKET_API_TOKEN: Bitbucket personal access token (PAT)

Set them:

export BITBUCKET_SERVER="https://bitbucket.globaldevtools.bbva.com/bitbucket/rest"
export BITBUCKET_API_TOKEN="YOUR_TOKEN"

Quick sanity check

bbdc doctor

If this succeeds, your base URL + token are working.

⸻

Usage

Show help:

bbdc --help
bbdc pr --help

List pull requests

List open PRs in a repo:

bbdc pr list --project GL_KAIF_APP-ID-2866825_DSG --repo mercury-viz

Output raw JSON:

bbdc pr list -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz --json

Get a pull request

bbdc pr get -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123

Create a pull request

bbdc pr create \
  --project GL_KAIF_APP-ID-2866825_DSG \
  --repo mercury-viz \
  --from-branch feature/my-branch \
  --to-branch develop \
  --title "Add viz panel" \
  --description "Implements X"

Add reviewers (repeat --reviewer):

bbdc pr create \
  -p GL_KAIF_APP-ID-2866825_DSG \
  -r mercury-viz \
  --from-branch feature/my-branch \
  --to-branch develop \
  --title "Add viz panel" \
  --description "Implements X" \
  --reviewer some.username \
  --reviewer other.username

Note: reviewer identity fields can vary by Bitbucket version/config.
This CLI uses {"user": {"name": "<reviewer>"}}. If your server expects a different user key
(e.g. slug), adjust the implementation in bbdc_cli/__main__.py.

Create as draft (only if your Bitbucket supports it):

bbdc pr create ... --draft
# or explicitly disable:
bbdc pr create ... --no-draft

Comment on a pull request

bbdc pr comment -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 \
  --text "LGTM. One nit: ..."


⸻

Troubleshooting

BITBUCKET_SERVER must end with '/rest'

Use the REST base, not the UI URL. For instances hosted under /bitbucket, the REST base is often:
	•	UI: https://host/bitbucket/...
	•	REST: https://host/bitbucket/rest

Unauthorized / 401 / 403
	•	Token missing or incorrect
	•	Token lacks required permissions for that project/repo
	•	Your Bitbucket instance may require a different auth scheme (rare if PAT is enabled)

404 Not Found

Usually one of:
	•	Wrong BITBUCKET_SERVER base path (/rest vs /bitbucket/rest)
	•	Wrong --project key or --repo slug
	•	PR id doesn’t exist in that repo

⸻

Development

Run without installing:

python -m bbdc_cli --help

Or run the entrypoint function:

python -m bbdc_cli doctor


⸻

License

Mercury - BBVA


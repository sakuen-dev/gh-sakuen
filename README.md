# gh-sakuen

A [GitHub CLI](https://cli.github.com) extension that puts `sakuen-dev` repos online at `<name>.sakuen.org` and looks after them, from the terminal.

## Install

You need the GitHub CLI, logged in with `gh auth login`. Then:

```bash
gh extension install sakuen-dev/gh-sakuen
```

Update later with `gh extension upgrade sakuen`. On Windows, run it from Git Bash.

## Put an app online

From inside a clone of your `sakuen-dev` repo:

```bash
gh sakuen init
```

It walks you through everything and suggests an answer for each question, so you can mostly press Enter.

1. Works out your build pack, port and start command from your files.
2. Asks for a subdomain and whether pushes should redeploy automatically (default no).
3. Reads variable names from your `.env`, and copies their values into the repo's GitHub secrets. Values never appear in the request.
4. Writes `.github/workflows/sakuen-deploy.yml`, then commits and pushes it.
5. Opens the deploy request in `sakuen-dev/infra`.
6. Follows the request, sends your secrets when the bot asks for them, and stops when the app is live.

Want to see what it would do first? Run `gh sakuen init --dry-run`. Add `--yes` to accept every suggestion.

## Day to day

| Command | What it does |
|---|---|
| `gh sakuen deploy` | Rebuild and redeploy from your branch. Live 2 to 5 minutes later. |
| `gh sakuen status` | Whether the app is running, and its last 5 deploys |
| `gh sakuen logs` | Last 200 lines your app printed. Private repos only. |
| `gh sakuen restart` | Restart without rebuilding |
| `gh sakuen rollback` | Go back to the previous version |
| `gh sakuen sync` | Copy values from `.env` into GitHub secrets, send them to the app, then redeploy |
| `gh sakuen watch` | Follow your deploy request again, for example after fixing a `failed` one |

Each command runs your repo's **Sakuen deploy** workflow and prints its result, so everything also shows up in your repo's **Actions** tab.

## When something goes wrong

The full guide, including troubleshooting, is in [sakuen-dev/infra](https://github.com/sakuen-dev/infra#readme).

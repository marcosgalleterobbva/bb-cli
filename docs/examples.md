# Examples

These examples use a fictional project `GL_KAIF_APP-ID-2866825_DSG` and repo `mercury-viz`.

## Review a PR end-to-end

```bash
# List open PRs
bbdc pr list -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz

# Get a specific PR
bbdc pr get -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123

# Add a comment
bbdc pr comments add -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 --text "LGTM"

# Approve
bbdc pr approve -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123

# Complete review
bbdc pr review complete -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 \
  --comment "Reviewed" --status APPROVED
```

## Add reviewers to an existing PR

```bash
# Add one reviewer
bbdc pr participants add -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 \
  --user alice --role REVIEWER

# Replace reviewers list
bbdc pr update -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 \
  --reviewer alice --reviewer bob
```

## Apply a code suggestion from a comment

```bash
# Fetch comment details (to find suggestion index and version)
bbdc pr comments get -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 456

# Apply suggestion index 0
bbdc pr comments apply-suggestion -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 456 \
  --suggestion-index 0
```

## Work with blocker comments (tasks)

```bash
# Add a blocker comment
bbdc pr blockers add -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 --text "Please fix tests"

# List blocker comments
bbdc pr blockers list -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123

# Resolve a blocker comment (requires comment version; auto-fetched if omitted)
bbdc pr blockers update -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 789 --state RESOLVED
```

## Inspect diffs and changes

```bash
# Raw PR diff
bbdc pr diff -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123

# Diff for a file
bbdc pr diff-file -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 src/main.py

# Diff stats summary for a file
bbdc pr diff-stats -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 src/main.py

# Changes with comment counts
bbdc pr changes -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 --with-comments
```

## Rebase and merge

```bash
# Check whether rebase is possible
bbdc pr rebase-check -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123

# Rebase (auto-fetches PR version)
bbdc pr rebase -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123

# Merge with a message
bbdc pr merge -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 123 --message "LGTM"
```

## Find PRs for a commit

```bash
bbdc pr for-commit -p GL_KAIF_APP-ID-2866825_DSG -r mercury-viz 8d51122def56
```

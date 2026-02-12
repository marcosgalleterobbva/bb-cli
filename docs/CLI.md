# CLI Reference

This is the authoritative command reference derived from `bbdc_cli/__main__.py`.

Global:

```
bbdc doctor
```

Pull requests:

```
bbdc pr list --project <KEY> --repo <SLUG> [--state OPEN|DECLINED|MERGED|ALL] [--direction INCOMING|OUTGOING]
             [--limit N] [--max-items N] [--json]

bbdc pr get --project <KEY> --repo <SLUG> <pr_id>

bbdc pr create --project <KEY> --repo <SLUG> --from-branch <name> --to-branch <name>
               --title <text> [--description <text>] [--reviewer <user> ...]
               [--draft|--no-draft] [--json]

bbdc pr comment --project <KEY> --repo <SLUG> <pr_id> --text <text>

bbdc pr approve --project <KEY> --repo <SLUG> <pr_id>
bbdc pr unapprove --project <KEY> --repo <SLUG> <pr_id>

bbdc pr decline --project <KEY> --repo <SLUG> <pr_id> [--version N] [--comment <text>] [--json]

bbdc pr reopen --project <KEY> --repo <SLUG> <pr_id> [--version N] [--json]

bbdc pr merge-check --project <KEY> --repo <SLUG> <pr_id>

bbdc pr merge --project <KEY> --repo <SLUG> <pr_id>
              [--version N] [--message <text>] [--strategy <id>]
              [--auto-merge|--no-auto-merge] [--auto-subject <text>] [--json]

bbdc pr update --project <KEY> --repo <SLUG> <pr_id>
               [--version N] [--title <text>] [--description <text>]
               [--reviewer <user> ...] [--draft|--no-draft] [--json]

bbdc pr watch --project <KEY> --repo <SLUG> <pr_id>
bbdc pr unwatch --project <KEY> --repo <SLUG> <pr_id>

bbdc pr activities --project <KEY> --repo <SLUG> <pr_id>
                   [--from-id <id>] [--from-type COMMENT|ACTIVITY]
                   [--limit N] [--max-items N] [--json]

bbdc pr changes --project <KEY> --repo <SLUG> <pr_id>
                [--change-scope ALL|UNREVIEWED|RANGE]
                [--since-id <hash>] [--until-id <hash>]
                [--with-comments|--no-with-comments]
                [--limit N] [--max-items N] [--json]

bbdc pr commits --project <KEY> --repo <SLUG> <pr_id>
                [--with-counts|--no-with-counts]
                [--avatar-size N] [--avatar-scheme http|https]
                [--limit N] [--max-items N] [--json]

bbdc pr diff --project <KEY> --repo <SLUG> <pr_id>
             [--context-lines N] [--whitespace ignore-all]

bbdc pr diff-file --project <KEY> --repo <SLUG> <pr_id> <path>
                  [--since-id <hash>] [--until-id <hash>] [--src-path <oldpath>]
                  [--diff-type <type>] [--context-lines N] [--whitespace ignore-all]
                  [--with-comments|--no-with-comments]
                  [--avatar-size N] [--avatar-scheme http|https]

bbdc pr diff-stats --project <KEY> --repo <SLUG> <pr_id> <path>
                   [--since-id <hash>] [--until-id <hash>] [--src-path <oldpath>]
                   [--whitespace ignore-all]

bbdc pr patch --project <KEY> --repo <SLUG> <pr_id>

bbdc pr merge-base --project <KEY> --repo <SLUG> <pr_id>

bbdc pr commit-message --project <KEY> --repo <SLUG> <pr_id>

bbdc pr rebase-check --project <KEY> --repo <SLUG> <pr_id>

bbdc pr rebase --project <KEY> --repo <SLUG> <pr_id> [--version N] [--json]

bbdc pr delete --project <KEY> --repo <SLUG> <pr_id> [--version N] [--json]

bbdc pr for-commit --project <KEY> --repo <SLUG> <commit_id>
                   [--limit N] [--max-items N] [--json]
```

Participants:

```
bbdc pr participants list --project <KEY> --repo <SLUG> <pr_id>
                         [--limit N] [--max-items N] [--json]

bbdc pr participants add --project <KEY> --repo <SLUG> <pr_id>
                        --user <username> [--role AUTHOR|REVIEWER|PARTICIPANT] [--json]

bbdc pr participants remove --project <KEY> --repo <SLUG> <pr_id> <user_slug>

bbdc pr participants status --project <KEY> --repo <SLUG> <pr_id> <user_slug>
                           --status UNAPPROVED|NEEDS_WORK|APPROVED
                           [--last-reviewed-commit <hash>] [--version N] [--json]

bbdc pr participants search --project <KEY> --repo <SLUG>
                           [--filter <text>] [--role AUTHOR|REVIEWER|PARTICIPANT]
                           [--direction INCOMING|OUTGOING]
                           [--limit N] [--max-items N] [--json]
```

Comments:

```
bbdc pr comments add --project <KEY> --repo <SLUG> <pr_id> --text <text>

bbdc pr comments list --project <KEY> --repo <SLUG> <pr_id>
                      --path <file_path>
                      [--from-hash <hash>] [--to-hash <hash>]
                      [--diff-types <list>] [--states <list>] [--anchor-state ACTIVE|ORPHANED|ALL]
                      [--limit N] [--max-items N] [--json]

bbdc pr comments get --project <KEY> --repo <SLUG> <pr_id> <comment_id>

bbdc pr comments update --project <KEY> --repo <SLUG> <pr_id> <comment_id>
                        [--text <text>] [--severity NORMAL|BLOCKER] [--state OPEN|RESOLVED]
                        [--version N] [--json]

bbdc pr comments delete --project <KEY> --repo <SLUG> <pr_id> <comment_id>
                        [--version N]

bbdc pr comments apply-suggestion --project <KEY> --repo <SLUG> <pr_id> <comment_id>
                                 --suggestion-index N
                                 [--comment-version N] [--pr-version N]
                                 [--commit-message <text>] [--json]

bbdc pr comments react --project <KEY> --repo <SLUG> <pr_id> <comment_id> --emoticon ":+1:"

bbdc pr comments unreact --project <KEY> --repo <SLUG> <pr_id> <comment_id> --emoticon ":+1:"
```

Blocker comments:

```
bbdc pr blockers list --project <KEY> --repo <SLUG> <pr_id>
                      [--states <list>] [--count]
                      [--limit N] [--max-items N] [--json]

bbdc pr blockers add --project <KEY> --repo <SLUG> <pr_id> --text <text> [--json]

bbdc pr blockers get --project <KEY> --repo <SLUG> <pr_id> <comment_id>

bbdc pr blockers update --project <KEY> --repo <SLUG> <pr_id> <comment_id>
                        [--text <text>] [--severity NORMAL|BLOCKER] [--state OPEN|RESOLVED]
                        [--version N] [--json]

bbdc pr blockers delete --project <KEY> --repo <SLUG> <pr_id> <comment_id>
                        [--version N]
```

Review:

```
bbdc pr review get --project <KEY> --repo <SLUG> <pr_id>

bbdc pr review complete --project <KEY> --repo <SLUG> <pr_id>
                        [--comment <text>] [--last-reviewed-commit <hash>]
                        [--status UNAPPROVED|NEEDS_WORK|APPROVED] [--json]

bbdc pr review discard --project <KEY> --repo <SLUG> <pr_id>
```

Auto-merge:

```
bbdc pr auto-merge get --project <KEY> --repo <SLUG> <pr_id>

bbdc pr auto-merge set --project <KEY> --repo <SLUG> <pr_id>

bbdc pr auto-merge cancel --project <KEY> --repo <SLUG> <pr_id>
```

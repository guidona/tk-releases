# Privacy

**tk sends nothing about you anywhere.** There's no telemetry, no analytics and no account. What it
reads stays on your machine and is shown only to you. This page lists what tk reads, what it writes,
and the few times it goes online.

## What tk reads

| What                                                                                                                                                                                           | Why                                                    | Where you see it       | Can be turned off                     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | ---------------------- | ------------------------------------- |
| Files and folders you open                                                                                                                                                                     | The viewer, the Explorer, note tabs                    | Those panes            | It only reads what you open           |
| Folders under `[rcd] roots` (names only)                                                                                                                                                       | `rcd` / `repo` jump to them                            | The picker, completion | Change `roots` / `exclude`            |
| Git repositories of your tabs                                                                                                                                                                  | The Git view, the branch in the status bar             | Git view, status bar   | Don't open the Git view               |
| Running processes (`/proc`)                                                                                                                                                                    | The Monitor, agent detection                           | Monitor, status bar    | —                                     |
| Your zsh history                                                                                                                                                                               | Alias suggestions                                      | The alias builder      | Settings → Privacy                    |
| Claude Code's session logs (`~/.claude/projects`) and the account name and email in `~/.claude.json`                                                                                           | Token usage                                            | Status bar, Monitor    | Settings → Privacy                    |
| The messages in the session log of a `claude` or `kiro-cli` running in one of your tabs (`~/.claude/projects/`, `~/.kiro/sessions/`) (your prompts, its replies, tool calls and their results) | The Session pane beside that tab                       | Session pane           | Settings → Privacy (`agent_sessions`) |
| An agent tab's folder's past session logs (the same files): your first message and how many, and the whole log of one you continue                                                             | The list to continue a conversation in a new agent tab | Agent tab              | Settings → Privacy (`agent_sessions`) |
| Which session a `claude` in one of your tabs has, and whether it's busy (`~/.claude/sessions/<pid>.json`)                                                                                      | Continue in an agent tab: the conversation to pick up  | Terminal tab menus     | Settings → Privacy (`agent_sessions`) |
| GitHub pull requests of your repositories (through `gh` and its login)                                                                                                                         | PR labels in the Git view                              | Git view               | Settings → Privacy                    |
| `~/.ssh/config` and what `ssh -G` says for each host, Docker / Podman containers                                                                                                               | The Remote pane                                        | Remote pane            | Don't open it                         |
| Your shell's PATH (asked of your login shell at startup)                                                                                                                                       | Commands you installed work in tabs                    | —                      | —                                     |

### What tk never reads

Credentials: `~/.claude/.credentials.json` and other tokens, SSH private keys, `~/.netrc`,
`~/.git-credentials`, cloud credentials (`~/.aws/credentials`, Kubernetes and Docker configs), your
GnuPG and password stores, browser cookies. A test in tk fails if
tk's code names any of them. Logging in to GitHub, SSH hosts or containers happens in `gh`, `ssh` and
`docker` themselves; tk never sees a key. The one password tk handles is one you type in the Remote
pane for a background SSH connection: it's handed to `sshpass` on a file descriptor, and kept only if
you tick Remember, encrypted with your system keyring (see below).

## What tk writes

All in your home folder, all yours to read or delete:

| File                                                                   | What                                                                                                                                                   |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `~/.config/tk/config.toml`, `aliases.toml`, `zsh/`, `omz/`, `p10k.zsh` | Your settings, aliases and tk's shell setup                                                                                                            |
| `~/.cache/tk/dirs.idx`                                                 | The folder index (names only)                                                                                                                          |
| `~/.local/share/tk/frecency.tsv`                                       | Folders you visit and how often, for `rcd`                                                                                                             |
| `~/.local/share/tk/session.json`                                       | Your open tabs, to reopen them (`[terminal] restore_tabs`)                                                                                             |
| `~/.local/share/tk/notes/`                                             | Your quick notes                                                                                                                                       |
| `~/.local/share/tk/trusted-folders.json`                               | Folders you trusted for agent tabs                                                                                                                     |
| `~/.local/share/tk/trusted-definitions.json`                           | Workflow files you approved, with a hash of each one's content                                                                                         |
| `~/.local/share/tk/app/`                                               | The window's own browser data (layout preferences)                                                                                                     |
| `~/.local/share/tk/ssh.json`                                           | Background SSH connections: the default authentication, each host's type and authentication if you chose one                                           |
| `~/.local/share/tk/ssh-credentials.json`                               | SSH passwords you chose to remember, encrypted with Electron's safeStorage (your system keyring); delete it to forget them all                         |
| `~/.ssh/config` (or a file it includes)                                | A host you add, and the multiplexing options you save in SSH settings; the file before each change is kept as `<file>.tk-backup`                       |
| `~/.local/state/tk/runs/`                                              | What workflow and agent runs did (commands, output, exit codes), the newest `[runs] keep` per one; secrets are replaced by `[redacted]` before writing |

## When tk goes online

- **Agent tabs:** tk sends nothing itself. What you type goes to Claude Code, which talks to Anthropic
  under your own login and settings, as it does in a terminal.
- **Update checks:** once a day, and when you open **Updates**, tk asks GitHub's API for the latest
  release (turn the daily check off in **Updates**). Downloads come from GitHub Releases.
- **GitHub pull requests,** through `gh`, while the Git view is open (turn off in Settings → Privacy).
- **Shell setup,** the first time and on `tk shell setup --update`: Oh My Zsh and plugins that don't
  ship with tk are downloaded from GitHub.
- **Markdown you view** may contain images on the web; showing them fetches them.
- **Report a problem** opens a new issue on tk's public tracker
  ([guidona/tk-releases](https://github.com/guidona/tk-releases)) in your browser (or a mail to tk's
  maintainer in your mail app, or saves the report as a file where you choose), filled in with what
  you wrote and the app's details (versions, OS, GPU; no file names or tab contents). The last lines
  of tk's log go in only when you tick them, after you've seen them (or when you set `[logging]
include_in_reports`). Nothing is sent until you submit the issue or send the mail yourself, and an
  issue is public: you see all of it on GitHub first.

## tk's log

tk writes a log of what goes wrong to `~/.local/state/tk/logs/main.log` (or the folder in
`[logging] dir`), rotated at a size you choose. It stays on this machine: nothing reads it but you
and Report a problem, when you include it.

- **In it:** startup (versions, OS, session type), IPC messages refused or failing, window errors,
  failed `tk` core calls (the subcommand and its error, not its other arguments), agent processes
  starting and ending (and the end of their error output when they fail), update checks and
  downloads.
- **Never in it:** commands, tab output, file contents, agent conversations, settings' values.
- **Masked before writing:** your home folder (as `~`), email addresses, and GitHub, Anthropic,
  OpenAI, Slack, AWS and bearer tokens.
- **The flight recorder:** the last 500 lines at every level, debug included, kept in memory only
  (never written). Report a problem includes them, so a report has the detail of a silent failure
  even when the file logs less.
- **Incidents:** when something goes wrong (an uncaught error, the window's process ending, a
  request from the window that fails) or tk didn't quit last time, tk saves the error, its stack
  and the log lines from just before it to `incidents/` in the log folder (the newest 20, masked the
  same way) and a notice offers to report it, once per kind of error per run
  (`[logging] notify_errors` turns the notices off). Nothing is sent: Report a problem lists them.
- **Crash dumps:** if tk itself crashes, Electron's crash reporter writes a native crash dump
  (Crashpad's `.dmp`) under `~/.local/share/tk/app/Crashpad`. It's never uploaded; it can hold some of
  the crashed process's memory, so attaching it to a report is your choice.

Everything else (SSH, containers, git remotes) happens through your own tools: in your terminal, or,
for background SSH connections you start in the Remote pane, your `ssh` run in the background.

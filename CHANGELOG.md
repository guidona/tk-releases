# Changelog

All notable changes to tk are documented here.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow
[Semantic Versioning](https://semver.org/).

## [Unreleased]

## [0.14.0] - 2026-11-22

### Added

- **A log for troubleshooting**, and problem reports by email: tk logs what goes wrong (IPC failures,
  window errors, failed core calls, agents ending, updates) to `~/.local/state/tk/logs/main.log`, with
  your home folder, emails and tokens masked, and never commands, output or conversations. **Report a
  problem** sends a report to the maintainer from your mail app, or saves it where you choose; the log's
  last lines go in only when you tick them, shown first. **Settings → Logging** sets the level, the
  folder, the size before a new file and how many old files to keep. When something goes wrong, tk
  saves the error with the log lines from just before it and a notice offers **Report…**, once per kind
  of error; if tk didn't quit cleanly, the next start offers to report that. A flight recorder keeps the
  last 500 lines of every level in memory, so a report has the detail of a silent failure too; native
  crash dumps stay on your machine.

- **Agents and notes in splits**: the Split menu lists Terminal, Note and Agent, each with a button
  to split right and one to split down, and it's in every right-click menu of a tab: in a terminal, in
  an agent's conversation or message box, in a note's editor, and on the tab itself. Ctrl+Shift+D /
  Ctrl+Shift+Alt+D also split agent tabs (a shell beside them, in their folder); in a note they stay
  the editor's. Each split has its header with its own name and icon, and the split you're in is marked in its kind's colour (an agent's own, a note's teal). In a narrow split or window, an agent's message box hint is cut with an ellipsis instead of clipped. A note's split comes back after
  a restart.
- **Zoom and pan the workflow canvas**, as in Obsidian: Ctrl+scroll or a pinch zooms round the pointer, from
  25% to 300%, to read a node up close; drag empty space to move around; the zoom bar in the corner (−,
  the percentage for 100%, +) and the keys +, − and 0 do it too. The dot grid zooms and moves with it.
  Hover a step's name or command for all of it, however much the node cuts off.
- **Open in dev container**: right-click a folder that has a `.devcontainer/devcontainer.json` (or
  `.devcontainer.json`) in the Explorer, or the Explorer's ⋯ for the folder it shows. A new tab builds
  and starts the container with the devcontainer CLI, its output in view, then opens a shell inside; the
  container shows in the Remote pane with its devcontainer tag. Without the CLI, the tab says how to
  install it.
- **Vim keys** in note tabs and the file viewer, off by default: the **Vim** button in a note's toolbar,
  Ctrl+Shift+Alt+V (or Vim keys in the palette), Settings → Editing, or `[editor] vim = true` in config.toml, switched without reopening anything.
  Notes get Vim's modes, motions, operators, registers, marks, search and `:s`; `:w` saves, `:q`
  closes (asking when unsaved), `:wq` both; yanks reach the system clipboard. In the read-only code
  view they move, search and copy; B, D, W, N and P there are Vim's while it's on.
- Tab groups in the **Monitor**: the Tabs section shows each group as a row with its dot, name, how many
  tabs it has and their CPU, memory, disk and processes together, its tabs under it with their own
  figures; click the row to fold it. Sorting orders groups by their totals and the tabs within each;
  tabs outside a group show as before.
- **Screenshot** of a terminal: Ctrl+Shift+S (or right-click → Screenshot → Copy) copies what the tab or
  split shows as an image, at the display's pixel ratio; **Save as PNG…** (also in the palette) saves it
  to a folder you pick as `tk-<tab>-<date>-<time>.png`. A notice says it was copied or saved, or why
  not.
- **Change any keyboard shortcut**: in Keyboard shortcuts (F1), click one and press the new keys, or
  Backspace to turn it off. A key another action has is refused with that action's name; the reset
  arrow (or Reset all) brings the default back. Changes apply at once, are kept in config.toml's new
  `[keys]` table (which you can edit too), and show in the palette, menus and tooltips.
- A tab group's **Colour** is a row of swatches in the theme's own shades instead of a list of names:
  the current one ringed, its name under the row, and the one under the pointer (or picked with the
  arrows) shown on the group's chip and sheet bar before you click or press Enter.
- **All at once** for Docker and Podman in the Remote pane: the ⋯ on an engine's header (or right-click
  it, or All Docker in a container's menu) stops every running container, removes the stopped ones or
  all of them, removes unused images or volumes, or purges everything unused. Each asks first and shows
  the command; a prune says how much space it freed.
- An **.rpm** for Fedora, RHEL and their relatives: `sudo dnf install ./tk-<version>-x86_64.rpm`. Like
  the .deb it runs sandboxed and puts `tk` and `tk-app` on the PATH, and the app menu's Updates
  downloads the next .rpm and offers `sudo dnf install`.
- Agent tabs offer Claude Code's **Auto** permission mode, as a terminal `claude` does: Claude Code
  approves safe actions itself and asks only for risky ones, so far fewer questions than Ask. Its tab
  gets the same peach line as Accept edits.
- **Tab groups**: drop a tab onto another to group them (or right-click → New group from this tab). A
  group is one compact chip in the top bar: a dot in its colour, its name, and how many tabs it has.
  Its tabs are sheets sized to their names in a slim bar above the status bar, shown whenever the
  group is, even with one tab; the + at its end adds a tab to the group (right-click for a note or an agent). Other new
  tabs stay out of groups.
  Drag sheets to reorder them, back to the top bar to take one out, or a tab onto a group's chip to add
  it; Move to group and Remove from the tab menu do the same. Double-click a chip to rename it;
  right-click it for its colour, Ungroup, or closing its tabs (asked once). The chip's badge is ringed
  when an agent in the group works (blue) or waits for you (pulsing peach). Alt+1…9 and
  Ctrl+Alt+PageUp/PageDown count a group once. Groups come back after a restart.
- Reviewing changes: **±** in the Explorer (or C) lists just the repository's changed files, and the
  filter narrows them; in the viewer, **↑** and **↓** beside a changed file's status step through its
  changes (as N and P do), centred, round to the first after the last.
- Drag a branch's label onto another branch in the Git view to **merge** it in or **rebase** it on
  top; it asks first, like the menus.
- The Git view marks a branch checked out in another worktree with its folder, and the agent working
  there when an agent tab is; click it to go to that agent tab, or open a terminal in the folder.
- **Suggest** in the Git view's commit box: the agent working in that repository (or your default
  one) writes a commit message for the picked changes, in the repository's style. It's asked once,
  with its tools off, and the message lands in the box for you to edit; nothing is committed on its
  own. The message box now takes several lines: Enter commits, Shift+Enter starts a new line.
- Conflicts in the Git view: when a merge, rebase, cherry-pick or revert stops, the uncommitted
  changes say which (a rebase with its step, 2 of 5) and list the files in conflict first. On a
  conflicted file, **Take ours**, **Take theirs** or **Mark resolved** (each says which side is
  which, as a rebase swaps them), then **Continue** or **Abort**.
- **Undo** after a Git view action that moved the branch (a commit, amend, cherry-pick, revert,
  merge, rebase, reset or pull): it goes back to the commit before, a commit's changes uncommitted
  again and anything you changed since kept. Not offered once the commit is pushed, and it won't run
  if the branch moved since.
- Commit part of a file from the Git view: in the uncommitted changes, click a change's + or − to leave
  that line out, or a hunk's **Leave out** for all of it, so you can keep one change an agent made and
  drop the next. The file's box shows it's in part, and the rest stays uncommitted; what you had staged
  for other files stays as it was.
- **Splits**: Ctrl+Shift+D puts a second shell beside the current one in the same tab,
  Ctrl+Shift+Alt+D under it (also in the tab's and the terminal's right-click menus). Alt+arrows
  move between splits, dragging the line between them shares the room, Ctrl+Shift+W closes the split
  you're in, and the status bar, side panes and Monitor follow it. Splits come back after a restart.
  **Typing into several tabs**: Ctrl+Shift+Alt+B marks a tab or split, and what you type in one
  marked tab goes to all of them; each has a peach line along its top and a badge, the status bar
  counts them, and Ctrl+Shift+Alt+S stops.
- Each split has a **header**: the program running in it (or the shell) and its folder, then
  **split right**, **split down**, **maximize** (that split fills the tab, the others keep running
  behind it; going to another split restores them) and **close**. Click the header to go to that split.
  Drag the **grip** in its middle onto another split to move it there: the half you drop on (left,
  right, top or bottom) shows where it goes, Esc cancels, and its shell keeps running.
- **Continue in an agent tab**: a `claude` running in a terminal tab hands its conversation to a new
  agent tab in its folder, from the tab's or the terminal's right-click menu or the command palette.
  `claude` quits in the terminal (tk asks first if it's in the middle of a turn), and the agent tab
  shows the whole conversation and goes on from there. The other way, **Continue in a terminal** in a
  Claude agent tab's menu ends it and runs `claude --resume` on the conversation in a new terminal tab.
- A **pin** in each side pane's header keeps that pane open in every tab you go to, and after a
  restart, until you unpin it or close it.
- Kiro tabs show how full the session's context is, as Kiro reports it, and the credits the
  conversation has used. The context is a small ring that fills (amber from 80%) in the agent tab's
  status line and the Session pane, for Claude Code too.
- A **command palette**, Ctrl+Shift+P: any action by name with its shortcut, the tk menu's pages,
  the folders you visit most (opens a tab there), your aliases (typed into the terminal), SSH hosts
  and containers. What you picked lately comes first. **F1** shows the keyboard shortcuts.
- A welcome on the first launch: whether tk's zsh is set up, the four things you'll do most with
  their shortcuts, and a way to the keyboard shortcuts. It stays in the tk menu as **Welcome**.
- For development: screenshot tests of the main panes, and a coverage floor for the core and the
  app's unit tests that CI enforces.

### Changed

- **Report a problem** is tighter now that reports can be public. Paths keep only the file's name, URLs
  only their host, and IP addresses, host names, this machine's, your login's and your SSH hosts' names,
  credentials in URLs, `password=`-style values and more kinds of tokens (Google, npm, GitLab, Stripe,
  JWT) are masked. **Send** asks before posting, needs a description or a picked error, and can't post
  the same report twice; the log is asked for on each report (not carried over) and can be edited before
  it goes. Send uses the system's proxy. Opening the report reads only the end of the log, and a run
  that keeps failing in new ways saves and offers only so many. Log files are yours alone. The relay
  shows what happened as text (no links or images), takes only JSON and has a cap for everyone together.
  The public changelog drops the private issue numbers and file links it had left. Its layout is new:
  what happened, the related error as cards, what's attached as rows you can open, and **Send** with
  **Other ways** (GitHub, email, save, copy) in the footer.
- **Report a problem** sends reports to tk's public tracker,
  [guidona/tk-releases](https://github.com/guidona/tk-releases), as issues: **Send** posts it in one
  click, no GitHub account needed (through tk's report relay; what you see in the dialog and nothing
  else), and **Open an issue on GitHub** fills in the same issue in your browser. Copy, Save report…
  and Send by email stay. The tracker also has each release's notes, the changelog, the privacy notes
  and a way to report security problems privately; it holds no code.
- Your message heading an agent's turn is a quiet card in regular weight, not bold text with a dot.
- Markdown headings in the view pane are in the text's colour, set apart by size and weight, as in an
  agent's reply (no longer peach).
- An agent's **branch** on its status line is a menu: switch to another local branch (once the agent is
  done), or open the Git view. The line's menus, carets, branch icon and context ring sit on one centre
  line, the send button is an icon and **Send** centred on the input, and the board's card shows the
  mode as a small pill and its agent's colour as a straight bar (not a border bent round its corners).
  Your message heading a turn is a size smaller, its dot on the first line.
- The sheet bar's + offers **New terminal**, **New note** and **New agent**: it's in the group's own
  bar, so "in this group" went.
- The window's text is back to Ubuntu Sans's full width; only the status bar stays narrower. The 90%
  everywhere read too tight once the font shipped with tk and applied on every system.
- An agent conversation reads more clearly: your message in bold behind the agent's dot, the answer in
  larger type and the steps that led to it smaller and dimmer, the folded work as a pill (blue while it
  runs), files and code as soft fills instead of outlines, code and diffs in framed wells, and a rounder
  composer that rings while you type.
- A long agent conversation gets an **outline**: from four turns, a row of chips above the thread, each
  turn's first words; click one to go to that turn, and the one in view is marked.
- While an agent works, one line at the bottom of its turn says what it's doing now: "Editing
  signup.tsx · 1.4 KB…", "Running npm test · 12s", "Thinking…", or in peach "Waiting for you · asked
  4s ago", so a turn's state shows without unfolding its work.
- An agent turn's unfolded work reads at a glance: its steps on a thin rail through their status dots;
  reads or searches in a row as one line
  ("Read signup.tsx, auth.ts +4 files", open it for each); a command with how it ended and how long it
  took ("Tests: 18 passed · 9s").
- Each turn of an agent conversation is one flat section, a hairline between turns: your message at the top, the agent's answer as its body,
  the files it changed as chips (click one to see it), and the turn's time and cost. Its work (steps,
  thinking, what it said along the way) stays open while it runs and folds to one line when the turn
  ends: "Worked 1m 12s · Read 6 files, edited 3 files, ran 2 commands".
- Agent tabs feel livelier while Claude works: a reply appears at a steady pace instead of in bursts
  (as it arrives under reduced motion), a tool call shows as soon as Claude starts it, with its file or
  command and how much it has written so far, and a running step shows how long it has taken.
- A tab group's chip is quieter: a dot in the group's colour, its name, and how many tabs it holds in
  grey figures, instead of a solid coloured number badge; an agent working or waiting rings the dot.
  A group's sheet bar shows even when it holds one tab.
- Dialogs share one box, header and footer: the title (with a line under it when there's more to say)
  and × at the top, the buttons on the right at the bottom, the same corners and spacing everywhere.
- Text boxes, lists and numbers look the same in every form and dialog (Settings, SSH, schedules and
  limits, the agents board, workflows, aliases, the Git view's confirm bar): one height, border and
  corner. The board's agent picker was a system dropdown; Settings' font preview sits under its list.
  The Monitor, Session and Agents panes have the same header as the others.
- The Git view's header is the side panes' header: its title, tools and ‹ back button line up with
  the other panes'.
- Waiting, empty and failed look the same in every pane: a quiet line on the pane's edge that breathes
  while something loads (off with reduced motion), and a failure in red with what to do about it.
  Actions in a line of text ("Add a host", "Open") share one link style.
- Lists select the same way everywhere (Explorer, Remote, the Git view's commits, the Monitor's processes
  and services): a tint, and in the list you're in a stronger tint with a bar on its left edge, no
  more ring around the row. Small labels (a host's kind, a service's scope, a step's effect,
  Installed) share one look.
- Actions have plain names in the command palette and the shortcuts sheet (**Split right**, **Move tab
  left**, **Find in the output**…), without notes in brackets or after a colon; the palette still finds
  them by the words that were dropped. The tab menu and a split's header say just **Split right** and
  **Split down**.
- Sections fold the same way in the Monitor, Remote and Session panes: one header, the same height,
  title, chevron and count on the right, and a grip on hover where they can be dragged.
- A tab has one coloured line, at the top: an agent's permission mode (peach for Accept edits, blue
  for Plan) takes the place of the active tab's accent instead of adding a second line underneath.
- Code, diffs, hashes and paths use JetBrains Mono, shipped with tk, without ligatures or italic
  comments (the window's code font; the terminal keeps its own).
- Workflows take any kind of value, at any step. Inputs can be a **file**, **folder**, **link** or
  **list** as well as text, numbers, yes/no and choices; tk checks a file or folder exists before it
  runs. Each step has its own typed **inputs**, fed by a workflow input, another step's output or a
  value set on the step, each a variable in its command. A step can write a **file or folder** as an
  output (tk gives it the path) for the next steps to take. On the canvas, a step's inputs and
  outputs are rows you connect by dragging from an output to an input (or onto the step for a new
  one); an input nobody feeds shows its value, set in Details with **Browse…** for a file or folder.
  The run dialog has Browse too, **Fit** and Ctrl+scroll zoom the canvas, and the starters use the new
  style. Existing workflows with `env` keep working. Removing a connection from its card works again.
- Each workflow in the list has a **⋯** button, and right-click opens the same menu: run, edit, its last
  run, trust a project's, and **Move to the trash**.
- Right-click in a terminal is short again: what's under the pointer and the clipboard first, then
  **Split ▸**, **Open ▸** (Explorer, Git, Remote, Monitor, Aliases, a new tab) and **Close ▸** (the open
  side panes) as submenus that open on hover, click or →. A tab's right-click menu has **Split ▸** too.
- The dropdowns in Settings and the agent picker on the Agents board open in tk's own menu, like
  the rest of the window, instead of the system's list. Esc closes the list, not Settings.
- Tooltips are in tk's style, like its menus, instead of the system's grey boxes.
- The window's text is a little slimmer: Ubuntu Sans at 90% of its width in Settings, side panes,
  menus and tooltips, close to the status bar's 87.5%.
- Pull request badges in the Git view show drafts, and say merged, closed or draft in words as well
  as in colour.
- The Git view reads better: a diff's + and − sit in a column of their own with the code in full
  contrast on a clearer green or red, file names and details use the theme's text colours instead of
  one grey, the diff's buttons wrap instead of being cut off, and **Commit** is a solid button with
  Amend beside it. Double-click a file to open it: an uncommitted one in the editor at its first
  change, one in a commit in the viewer at that revision.
- The font size reaches past the terminal: side panes, agent conversations and notes scale with it,
  and **Ctrl+scroll** changes it like Ctrl+= and Ctrl+-, in any tab.
- Destructive actions ask the same way everywhere and say exactly what will happen: killing a process
  (from a menu or a tab's Kill all), removing containers, disconnecting a host. In the Git view, a
  hard reset, discarding changes (all, or one file), and deleting a branch, tag or stash offer
  **Undo** once done: tk keeps what it needs first (uncommitted changes, the old commit).
- Agent tabs: the model, agent, conversation and folder menus have a filter once they're long, and a
  long menu keeps a sensible height and scrolls instead of covering the window. The folder menu lists
  every folder you've visited (type to find one) and **Browse…** picks any folder.
- The Monitor's Claude section is now **Agents**: a card for each agent installed here (Claude
  Code, Kiro, Codex, Gemini CLI, Aider), with the tabs it runs in, an agent tab's context and
  credits, and Claude Code's usage as before. tk recognises agents from one list in the core, so
  the Monitor, the Processes badge and the notifications agree on what's an agent. `tk usage
--json` now prints `{ "agents": [{ id, name, installed, usage }] }`; Claude Code's usage is that
  agent's `usage`.
- The status bar shows the agent in the active tab: in a Kiro tab, Kiro with its context and
  credits instead of Claude Code's usage.

### Fixed

- In an agent tab, resting on an edited file's chip shows its first lines and a click opens it beside the
  conversation, as for files named in a reply: its line counts (`+2`) were read as part of its name, so
  nothing showed and the log had a `CHANGELOG.md+2` error. A turn's file chip still opens and closes
  its file once per click.
- Clicking into a split's terminal makes it the split you're in: its marker, the status bar and the side
  panes follow, not only a click on its header.
- The workflow canvas's dots and lines line up: every port is one size, centred on its node's edge, and
  each line ends at its dot (they stopped up to 25px short and a few pixels off their rows). The kind's
  bar stays clear of the ports, a selected node gets an accent border instead of a grey glare, and the
  Inputs and Outputs panels lose their bent coloured top edge. Ctrl+scroll over the canvas zooms it again
  instead of tk's font size.
- The workflow editor keeps its own width: stretching it no longer widens the Explorer and other side
  panes in every tab, nor does dragging those resize the editor.
- A working agent no longer costs a quarter to half a CPU core: its spinners, dots and pulses were endless
  animations that kept the window drawing every frame (about 52% of a core on Wayland with the agent in
  view, 25% out of view; now about 8% and 2.5%). Working shows as still blue dots and the seconds counting;
  the thinking dots light in turn once a second; waiting for you still pulses, once a second. The same goes
  for a running workflow and a command running in the status bar.
- A note's toolbar buttons have room between them, their labels look centred, and Save as… no longer
  breaks onto two lines in a narrow window.
- A workflow's nodes show their kind's colour as a straight bar inside the edge, like the agents board's
  cards, instead of a thick left border bent round the rounded corners.
- An agent's conversation keeps following its end when a reply's text is laid out a moment after it
  arrives: it used to stop short of the end and then stop following, and the outline marked the wrong
  turn.
- A screenshot of a tab that isn't shown says the terminal isn't on screen, instead of taking a few
  pixels of the window and saying it worked.
- The status bar is slim again outside Ubuntu: tk ships Ubuntu Sans, the window's font, instead of
  falling back on Fedora (and the like) to a font without the width axis that narrows it.
- In an agent tab, a command's output excerpt stays on one line beside it, cut short when it doesn't
  fit; it wrapped a word per line in a narrow column when the command was long.
- Kiro's permission questions read clearly: a short question with Allow, Always and Deny lined up under
  it (a long one stays two lines, all of it on hover), the command as a command whatever shape Kiro
  sends it in, and raw input only folded under Details. Board cards keep long questions short.
- tmux with its mouse mode on (and any program that asks for the mouse) gets right-clicks instead of
  tk's menu; Shift+right-click still opens tk's menu, and tk's comes back when the program lets go.
- The Monitor's Tabs section brings the current tab into view even when it's drawn before its list has
  a height; it could stay scrolled away from it.
- The × on a tab with splits (and middle-click, and the tab menu's Close tab) closes the whole tab, every
  split, asking first if something runs in one; it used to close only the first split. Close other tabs
  leaves the tab's own splits alone, and Ctrl+Shift+W says it closes the split you're in. The split
  actions say which way they go (side by side, one above the other), and the command palette also finds
  them by "horizontal" and "vertical".
- Continuing a long conversation in an agent tab showed its oldest part: tk read only the first 8 MB of
  its log. It now shows the latest part, and says earlier messages aren't shown.
- The Monitor pane no longer scrolls a little on its own as its sections update.
- Services a program starts with `systemd-run` (an app's background server, say) are named by their
  command, `foo-daemon serve`, not `[systemd-run]` and its full path, and get their app's icon
  instead of the OS logo. Icons an app installs in your home folder's icon theme are found too.
- A side pane dragged narrower than it can show scrolls sideways, so its buttons and columns stay in
  reach, instead of being cut off at the column's edge.
- Splits work with side panes: a split tab's side panes open once, at the edges of the whole tab,
  and follow the split you're in (a pinned pane no longer shows in every split). **Split down** in a
  side-by-side split now puts a shell under that one instead of adding another beside it, and
  Alt+arrows go to the split that's really there. Each split has a **×** in its corner on hover, and
  **Close this split** in its right-click menu.
- Opening a pane over the workflow editor (or a widened Git view or Monitor) no longer leaves the
  editor squeezed beside it: the new pane takes its place at the side's width, and reopening the
  editor brings it back wide, as you left it.
- The Monitor's Tabs section no longer grows with every tab: it shows 10 rows and scrolls, with the
  header and the totals kept and the active tab in view. The gear menu sets 5, 10 or 20 rows, or
  every tab, and the Monitor remembers the choice.
- The status bar's agent item (an agent tab's context and credits) no longer draws over CPU, RAM and
  GPU beside it.
- Agent tabs show Kiro's agents by name, not by id: `kiro_default` reads **Default** in the agent
  menu and the status line.
- The Monitor's sections fit a default-width side pane instead of being cut off on the right. A
  service's status opens as one block with its row (tinted red when it failed), with Start, Restart
  and Stop buttons; a service without an app icon gets a gear, so names line up, and the count says
  "4 services".
- Closing a menu with Esc puts the focus back where it was, so shortcuts work again without a click.
- The Monitor has no Claude section on a machine without Claude Code, as the status bar already
  had no Claude item there.

## [0.12.0] - 2026-11-05

### Added

- Settings → **Appearance**: themes. Catppuccin's Mocha, Macchiato and Frappé (dark) and Latte
  (light), or follow the desktop's light or dark preference as it changes (`[appearance] theme`). The
  window, terminals, the file viewer, notes and agent tabs all follow. The terminal's **font size** is
  remembered (`[terminal] font_size`: Ctrl+= and Ctrl+- save it too), and its **line height**,
  **cursor** (block, bar or underline) and **blinking** are settings.
- Remote pane: **background SSH connections and tunnels** without a terminal tab. A host whose config
  says `SessionType none` or `ForkAfterAuthentication yes` is a background host (a tunnel when it also
  has a `LocalForward`, `RemoteForward` or `DynamicForward`); its name is only a hint, and you can
  choose its type in **Connection settings…**. **Connect** logs in in the background and the host
  shows its state beside it: connected only once checked (its master answers `ssh -O check`, its
  forwards listen), connecting, needs a password, error, disconnecting. A connection started outside
  tk is seen too, and **Disconnect** asks before closing one others may share. A password is asked in
  a dialog (sshpass is the default; it gets the password on a file descriptor, never a command line),
  asked again when it's wrong or changed, and kept only if you tick Remember, encrypted with your
  system keyring. A new host key shows its fingerprints before you trust it; a changed one stops the
  connection. Wrong password, unknown or changed host key, network, configuration, a port in use and
  a missing sshpass each say what happened and what to do.
- Remote pane: **View SSH configuration…** shows what `ssh -G` says for a host and where each value
  comes from (file and line, the system's config, OpenSSH's default, or tk). **SSH settings** (the gear)
  sets the default authentication, whether tk shares one connection per host when your config doesn't,
  and ControlMaster, ControlPersist and ControlPath for every host (a `Host *` at the end of
  `~/.ssh/config`) or one Host block: set or unset, checked by `ssh -G` before it's written, and
  refused with the line that decides when an earlier entry would win.
- Agent tabs: work with Claude Code in tk's own interface instead of its terminal one. Ctrl+Shift+I
  (or **New agent** on the **+** button's right-click menu, or a tab's) opens one in the current
  folder. The conversation reads like a document: your messages start turns, replies stream in,
  each tool call is one line you can open (small edits show their diff), each turn ends with its
  time, cost and files changed, and Claude's permission questions are one line you answer with
  **Allow**, **Always** and **Deny** or y / a / n, with a notification when you're looking elsewhere.
  Beside it, the Session pane keeps the goal (your first message), Claude's plan, the history (click
  a turn to scroll back to it), every file changed and how full Claude's context is. A file the
  agent edits opens in the file viewer over it, with its changes marked; ‹ Session goes back. Esc
  stops the turn. The Session's sections fold and move, like the Monitor's. The **Agents** board
  (Ctrl+Shift+B, on any tab) lists every agent tab under Needs you, Working, Ready and Ended, with
  Allow and Deny right on a waiting one, and starts a new agent with its first message. A `claude`
  you run in a terminal tab gets the Session pane too, read from Claude Code's session log (Settings
  → Privacy can turn that off). tk runs the
  unmodified `claude` with your own login, and asks before the first agent in a folder, because
  Claude Code started this way runs the project's hooks and MCP servers without asking.
- Agent tabs work with Kiro too (`kiro-cli`, over the Agent Client Protocol), the same way as with
  Claude Code: with both installed, **New agent** and the Agents board ask which, and Ctrl+Shift+I
  opens the one you started last. A `kiro-cli` in a terminal tab gets the Session pane from its
  session log.
- In an agent tab, a `/` at the start of a message lists the agent's slash commands (Claude Code's,
  its skills and your own; Kiro's): ↑ ↓ to choose, Tab or Enter to fill one in.
- The Session pane's history has a filter, lists the last 50 turns (20, 100 or all from its ⋯ menu,
  which also hides sections) and scrolls in a height you drag. In an agent tab, the agent and the
  folder under the message box are menus to start another agent, or the agent in another folder.
- Agent tabs: a new one lists the folder's past conversations, and one click continues one. Undo on a
  turn's end puts back the files it edited (unless they changed since). The model is a menu under the
  message box, next to how full the context is (with Compact when it fills up). In the message box,
  `@` lists the folder's files, ↑ brings back what you sent, and images can be pasted or dropped in.
- Agent tabs, design: each agent has its colour (Claude Code peach, Kiro purple) on your messages, its
  tab and its board card; its thinking shows as one dim line you can open; a finished turn's reads,
  searches and commands fold into one line ("Read 4 files, ran 2 commands"); a new conversation
  offers a few things to ask and the prompts you saved for the folder (Save, on your message); the
  board's cards are denser, with a live line of what each agent does and its plan's progress.
- Agent tabs, features: Review on a turn's end shows its changes file by file, to undo one or all,
  or commit them in Git; a message sent while the agent works waits, shown above the box, to change
  or remove; an agent can work in a git worktree of its own (the folder menu, or the board's Own
  worktree), and the board can give the same task to every agent, each in its worktree; an agent's
  question notification has Allow and Deny on it (with `notify-send`); the Monitor shows the last
  30 days of Claude Code tokens and the folders that used the most.
- Agent tabs, round three: Ctrl+K opens the agent palette (new agents, model, review, undo,
  worktrees, schedules, limits, look); a file the agent names shows its first lines on hover and
  opens on a click; a compact view (messages and answers only, also on its own when narrow) and a
  light theme; Worktrees lists tk's, shows their changes, compares two side by side, brings one back
  (squashed and staged) or deletes it; the Session pane's Instructions lists the folder's AGENTS.md,
  CLAUDE.md and Kiro steering to edit; scheduled tasks start an agent at a time each day while tk
  runs; spending limits (a day's, a folder's) warn when agents pass them.
- Agent tabs: a reply reads as Markdown while it streams (headings, lists and code as they come, each
  finished block fading in) instead of turning into Markdown when it ends.
- Agent tabs: right-click in the conversation copies the selection, a reply (as text or Markdown),
  a command or a path, quotes the selection in your next message, or puts one of your messages back
  to change and send again; the message box has Cut, Copy, Paste and Select all.
- The Monitor opens on every tab: beside an agent's conversation and beside a note too (Ctrl+Shift+M
  or the activity bar), as does the Agents board on a note.
- The Monitor's Tabs section lists agent tabs too: their agent's processes, CPU and memory, and what
  the conversation says (working, waiting for you, ready) with its cost so far; right-click stops the
  agent.
- Nerd Font icons in a prompt (powerlevel10k, starship…) show in the terminal instead of empty boxes:
  tk ships the Symbols Nerd Font as its last fallback. The terminal's font is a setting too:
  `[terminal] font_family` in config.toml, or Settings → Terminal → Font.
- Agent tabs: a command the agent ran reads like one, in shell colours (the command, flags, strings,
  paths) on a light tint, and a file it edited is a chip with its name and the lines out and in; the
  gap after "Ran" and "Edited" is one space. Diffs of shell, TOML, Ruby and Lua files are coloured
  too.
- Agent tabs: slash commands work as in the agents' CLIs. `/model`, `/clear` and `/resume` (Kiro's
  `/chat new` and `/chat resume`) open tk's own model menu, a new conversation and the folder's past
  ones; commands that need the agent's own screen (`/agents`, `/config`, Kiro's `/agent create`,
  `/settings`…) open in a terminal tab; after a command, its subcommands are listed.
- Settings → Terminal → Font lists the monospace fonts you have (Nerd Fonts marked), with a preview of
  a prompt in the one you pick, instead of a box to type a name in.
- Agent tabs: a question's Allow, Always and Deny are smaller, on the question's own line (top right;
  under it when narrow), with the command or the change below; smaller on the Agents board too.
- Agent tabs: a command the agent ran is tinted more lightly, and at its clearest under the pointer.
- Agent tabs: code blocks in a reply are coloured like the file viewer's (as soon as each block is
  finished while it streams), and its headings take the text's colour, set apart by weight and size,
  instead of an orange-brown.
- An action that fails in the background (saving, refreshing, loading a diff, opening a link) says so in
  a short notice instead of failing silently, and the main process logs such failures.
- Small fixes from the code scan: the window declares its language (for screen readers), alias packs
  and shell plugins sort as people read them, and the IPC array check passes only the item to its
  validator.
- Side panes stack: opening one on a side where another is open puts it under that one (the Monitor
  under the Explorer) instead of closing it. A line between them shares the height (kept per pane),
  each closes alone, and F6 moves between them; the file viewer still covers the pane it opened from.
- Agent tabs get the Explorer and Git (Ctrl+Shift+E, Ctrl+Shift+G or the activity bar), on the
  agent's folder: follow what it changes (both catch up when a turn ends), open a file over the
  conversation, and mention a path in your message from the Explorer's menu.
- The Git view's actions (switch, merge, commit, push, stash…) run in the background, without a
  terminal or a free prompt, and show what git said; one that needs you (a password, a passphrase, an
  editor) says so and opens a terminal with it on a click. `[git] run_in_terminal = true` (or Settings)
  types them into the tab's shell as before.
- Agent tabs: the conversation's width is yours to set: drag its edge (double-click for the usual
  width), or pick Narrow, Medium, Wide or Full width in Ctrl+K → Look. A paste over 10 lines (or
  1000 characters) folds into a chip in the message box, to read, expand or remove; the agent gets it
  in full, and your message shows the chip.
- The Monitor's process filter takes `a | b` for either, `-word` for not, and `/regex/` (any case,
  spaces allowed), with the other terms: `user:root /sshd|cron/ -sftp`; an invalid regex is marked
  in red and says why.
- **Workflows**: pipelines of commands you run often, as YAML files you can read,
  review and keep in git: `~/.config/tk/workflows/`, a project's `.tk/workflows/` (it wins over
  yours, with a warning) or a package's. tk runs the steps as real processes, one at a
  time, in an order that comes from the file alone: pipes, `needs` and named values, ties in the
  order they're written; a cycle is an error that lists it. A failed step skips
  exactly what depends on it, and the run says why. A timeout or a cancel stops a step and
  everything it started. See docs/WORKFLOWS.md.
- Workflows are checked before they run, and every problem names its field and line: an unknown
  version, a bad step ID, `run` and `uses` together, a reference to a missing step, input, output or
  secret, an unknown tool, a timeout that isn't positive, a default of the wrong type; likely
  mistakes are warnings. Data reaches a script only through `env` (`"$NAME"`), never as
  `${{ … }}` inside `run`, so a value like `; rm -rf ~` stays a value. A step can pull
  typed values out of its output (`text`, `lines` with a filter, `json`, `kv`, `int`) for the steps
  after it and for the workflow's outputs, or call one of tk's tools (read a file, list a
  folder, inspect a process) with typed arguments instead of a script.
- What runs without asking: reads; a write step asks once per run; a destructive or `confirm` one
  every time, with its command and environment exactly as they'll run (**Run step**, **Skip step**,
  **Stop workflow**). A project's workflow runs once you trust its content, and a change asks
  again. Secrets live in your keyring and are redacted from everything tk records. Each run is recorded in `~/.local/state/tk/runs/` and exports as Markdown or JSON.
- From the terminal: `tk wf ls`, `tk wf run <id> name=value` (each step and its output as it runs,
  approvals inline, Ctrl+C cancels; `--yes`, `--json`; `--from <step> --run <run-id>` reruns from a
  step, `--only <step>` tests one), `tk wf validate`, `new`, `edit`, `trust`, `runs`, `report`, and
  `tk secret set`. Exit codes: 0, 1 failed, 124 timed out, 130 cancelled, 2 a problem with the file
  or the inputs.
- In the app: the **Workflows** pane lists yours and the project's by category with their last run,
  and follows a run step by step (state, time, exit code, command, output, why a step was skipped),
  with its progress and Cancel in the status bar; a past run opens from its record, reruns from a
  step or tests one. Ctrl+Shift+K (or **Workflows** in the status bar) finds one by name,
  ID or category and runs it, asking its inputs.
- The workflow editor: a canvas with a node per input and step (its kind, its effect, whether it
  asks; destructive ones stand out), pipes drawn solid, run-after dashed and named values dotted
  with their variables. Drag to move; drag from a node's edge to another to connect them; click a
  line to remove it. **Details** edits the selected step, checked as you type, and
  **Test this step** runs just it. **YAML** is the file itself: an edit applies as soon as
  it parses, and canvas edits rewrite the file the same way. Moving a node saves the
  layout beside the file (`.layout/<id>.json`), never in it.
- Agents can run your workflows: an agent tab gives Claude Code or Kiro each workflow you trust as a
  tool (`tk mcp`, an MCP server), with its inputs, outputs, description and steps. A call asks you
  once, like any tool; a destructive step still asks in tk with its command; the agent gets the
  outputs and the run ID.
- Starter workflows: **New workflow** (and `tk wf new <id> --starter <name>`) starts blank or from
  one of five: Diagnose Linux service, Diagnose production pods, Search large logs, Check server
  health and Restart failed services.
- For development: `make sonar` scans the code with a local SonarQube (`dev/sonar/`).

- Agent tabs: a permission mode menu next to the model, like Shift+Tab in a terminal `claude`: **Ask**,
  **Accept edits** (edits without asking; commands still ask) or **Plan** (reads and plans, changes
  nothing); Kiro's own modes when it offers them. The one you pick is kept for that folder, and a tab
  that asks less is marked, on its tab and its board card. A question now says what **Always** would
  save and where (a rule for one exact command says so).

- A default agent: `[agents] default` (Settings → AI agents) picks the agent Ctrl+Shift+I and **New
  agent** start, and puts it first in the New agent menus. An agent tab's tooltip names its agent.

- The Remote pane shows which SSH hosts tk is connected to, without a connection test: a green dot
  and "connected" (with the number of tabs), or "connection lost" when one dropped. Right-click a
  connected host to go to its tab or **Disconnect** (its tabs stay; Enter reconnects), a lost one to
  **Reconnect**. Hosts are sorted by name.

- A **Services** section in the Monitor: every systemd service, user and system, with its state and
  since when it runs or when it last ran; a failed one stands out. Filter it like the Processes list
  (words, `-not`, `a | b`, `/regex/`), show all, running, failed or watched ones, sort by name, state
  or since, and choose how many rows show. Each unit shows its description first ("CUPS Scheduler",
  not `cups.service`) and an icon that says where it comes from: its app's (from the app's desktop
  file, a startup app's or a snap's), your OS's logo for what the system installed, or a page for one
  you wrote yourself. Right-click a unit for its **Status**: its state, PID,
  memory and latest journal lines (newest first) open under its row, no terminal needed (the full journal can still
  open in a tab). Start, stop or restart it from the same menu: a system unit asks for your password
  in the desktop's own dialog, and only where there's none goes through `sudo` in a tab. **Watch** a
  unit to pin it at the top (`[monitor] services`).

- The Monitor, Remote and Session panes' sections are as tall as their content, up to a height of
  their own (the System and GPU charts are always whole); past it, a section scrolls on its own.
  The Monitor's Processes and Services share the room the other sections leave, more as you fold
  them, and only their rows scroll: the filter, the column headers and the row count stay put.
  Nothing else is stretched or squeezed, so there's no gap inside Processes and Claude is no longer
  cut off; when the sections don't all fit, the pane scrolls. The history no longer has its own
  corner to drag.

- Buttons look the same everywhere, and calmer: the main action is a purple tint with purple text
  instead of a solid purple block, a destructive one a red tint, the rest quiet. Checkboxes and radio
  buttons are drawn in tk's own style instead of the system's, and keyboard focus is a quiet light
  ring instead of a purple glow.

- Agent tabs, slash commands: Enter on a command in the list runs it when it takes nothing more
  (one that does, like `/review <pr>`, is filled in to finish); Alt+Enter runs it in a new agent tab,
  leaving the conversation as it is. A command you ran reads as one, and Claude Code's own answer
  (`/cost`, `/context`…) sits in a card instead of looking like Claude's reply; one it can't run here
  says so with **Open in a terminal**, and `/help` lists the commands.

- Workflow editor: drag the left edge of the Details, YAML and Run panel to make it wider or
  narrower (or focus it and press ← →); the width is kept, and double-click puts it back.

- Workflows can branch: a step's `if` runs it only when a condition holds, such as
  `${{ steps.check.stdout }} != active` or an input that's true. Otherwise it's skipped, with its
  condition as the reason, and so is what depends on it. `tk wf validate` checks the condition's
  references like any other expression, and a condition never reads secrets.
- The workflow editor, without YAML:
  - **Inputs and outputs** are rows in the workflow's Details: name, type, default, required and a
    description for each input (renaming one updates every step that uses it), and what a run
    gives back.
  - **Steps** come from **+ Add step**, which says what each kind does with an example. A step's
    Details lead with what it runs, its effect in plain words ("asks once per run"), **Run only
    if** and its outputs as rows; the rest is under Advanced.
  - **Insert value** in a command picks an input or an earlier step's value (with its type and,
    after a run, an example) and writes `"$NAME"` and its environment line for you.
  - **Connections**: drawing one asks what it does (pipe its output in, pass a value, or just run
    after it), and clicking one shows what it carries. A blank canvas explains the four parts:
    inputs, steps, connections, outputs.
  - **Right-click** a step for Edit, Edit the command, Add a condition, Test this step, Duplicate
    and Delete; an input for Edit and Delete; a connection to remove it; the canvas to add a
    step or tidy. The workflow's Inputs and Outputs sit in headed sections, coloured like their
    nodes on the canvas, and every field in them has its name above it.
  - **Named ports**: a step shows each output it declares on its right and each variable it reads
    on its left, connected or not. Drag from an output straight to a step to pass that value; a
    value's line runs from its output to its variable.
  - **The last run** shows on each step: how it went, its error in a sentence, its output and
    command. **Undo / Redo** (Ctrl+Z) cover every canvas and form change, and **Tidy** lays the
    steps out again.
- Workflows and agents: **New workflow → Describe it** has an agent tab draft the workflow from
  what you say it should do. It validates the draft and never runs it; you review it in the
  editor. In the editor, **Ask an agent** explains the workflow or diagnoses its last failed run.
- Git view: **N** and **P** step through a diff's changes (↓ ↑ in its header do too), on into the
  next or previous file; **]** and **[** go to the next or previous file. Clicking a change's header
  or a line number opens the file at that line, and **Open** opens it at the first change. In the
  file viewer, **N** and **P** go to the next and previous change since the last commit.
- Remote pane: right-click a container to **Restart** it, **Remove** it (`rm -f`; named volumes
  are kept) or **Remove stopped** Docker or Podman containers (`container prune`). Removing asks
  first and says what will go.

### Fixed

- A terminal tab running `kiro-cli` no longer always reads as idle in Monitor → Tabs, and the
  "may be waiting" notification follows it: an agent's activity counts the processes under it (Kiro's
  chat, a build it runs), not just its own.
- An agent tab can be renamed like a terminal tab: double-click it, or right-click → **Rename tab**;
  an empty name goes back to the agent and folder.
- tk no longer keeps a laptop's discrete GPU awake: the Monitor doesn't read an NVIDIA or AMD GPU that
  is powered down to save power (`nvidia-smi` woke it every 2 seconds) and shows it as asleep, and it
  stops sampling while the screen is locked or the system goes to sleep.
- Kiro's agents: their menu in an agent tab is called **Agent** (not Permissions), each a line with
  its description cut short (in full on hover), and picking one works with Kiro CLI 3, which lists
  them as a session config option (`session/set_config_option`); a model listed that way changes
  too.
- Monitor → Tabs: an agent's state ("kiro-cli working", "Claude working") is one slim line like the
  others; it took the agent tab's styles, as did the Processes table's **agent** badge.
- Remote pane: a tunnel to a server you're already connected to (a terminal tab, or another host of the
  same server sharing its connection) gets its forwards: **Connect** adds them to that connection
  (`ssh -O forward`) and **Disconnect** takes back only them (`ssh -O cancel`). It used to be shown
  connected without its ports.
- The side panes line up: Explorer, Aliases, Remote and Workflows share one header, one filter field
  and one empty state on the same edge, on a fixed scale of sizes and spacing. Aliases' actions
  are icons like the other panes', and the line between stacked panes is a hairline.
- Settings: a change left unsaved when the dialog closed was saved later with the next one. Closing
  now drops it.
- Remote pane: tk no longer overrides your SSH multiplexing. It used to add its own `ControlMaster`,
  `ControlPath` and `ControlPersist` to every ssh it ran, which replaced yours (so `ssh -O check` from
  another terminal didn't see tk's connections); now it adds them only for hosts your config sets
  none for, and Settings can turn that off.
- Monitor: the Processes and Services filters keep their focus and caret while you type: the Monitor's
  redraws (every sample) no longer take the lists out of the page. Services takes the same keys as
  Processes (`/` to the filter, ↓ or Enter to the rows, ↑↓ to select, Enter for a unit's status,
  Escape clears and then goes back to the list), folding a section with the focus in it leaves it on
  the Monitor, and a pane hidden to make room never keeps the focus.
- Monitor: **Stop** no longer fails silently. It waits a moment to see the process end, and if it
  ignored the request, its button (or menu) offers **Kill it** (SIGKILL). A paused process is resumed
  so it can quit, and a zombie or a process stuck in the kernel says why it's still listed.
- On Ubuntu 24.04+, the AppImage's **Sandbox off** now says what to do: install the .deb, which runs
  sandboxed. CI checks every push that the installed .deb is sandboxed there and the AppImage is on
  Fedora and Arch.
- A very long line in a workflow step's **Outputs** box no longer slows the editor down, and the
  terminal font list runs fontconfig's `fc-list` from `/usr/bin` only, never from a folder on your
  PATH. Workflows' logic is unit-tested, and the SonarQube quality gate passes.
- The Monitor no longer runs past the window's edge when its side pane is narrower than 480 px,
  which hid its right side and its gear.
- On a wide Monitor, the Claude section puts this window, today and the last 30 days side by side
  instead of stretching each across the window: the 30-day chart keeps thin bars instead of wide
  slabs. In the side pane they stay one under the other. **Today** reads like the window: its
  tokens, how it compares with your busiest and your average day, its breakdown, then by model.
- A side pane that was stacked with another, then shown alone, fills its side again instead of
  keeping the share of the height you'd dragged it to (the Session pane stopping two thirds down).
- Workflows: **New workflow** (+) and Refresh in the pane's header work while a workflow is open in
  the editor (+ asks you to save first when it has changes), and the New workflow dialog's starters
  read as a list again instead of being pushed off to the right.

## [0.11.0] - 2026-10-27

### Security

- The main process checks every request from the window:
  only tk's own page may ask, and each request's arguments are validated (types, sizes, absolute
  paths, ids); git revisions can't be passed as options. Note tabs save without asking only to your
  notes, `config.toml` and files you opened yourself; any other file asks once. Opening things from
  the output never runs a program. The window gets no browser permissions, and a tighter Content
  Security Policy.
- tk reports the Chromium sandbox's real state (from the renderer's seccomp filter), with a test that
  it matches what tk says.
- CI audits dependencies (`npm audit`, `cargo audit`) on every push.
- `SECURITY.md` says how to report a vulnerability; `docs/SECURITY.md` is tk's threat model and
  `docs/PRIVACY.md` lists what it reads and writes (it sends nothing).

### Added

- New icons for the activity bar (the pane icons on the left), drawn to scale, with a soft highlight
  for the open pane. Its size is a setting: Settings → Activity bar, or `[activity_bar] size` in
  config.toml (`"small"`, `"medium"` the default, `"large"`); the bar is wider and its icons bigger
  with it.
- Choose the files to commit in the Git view: each uncommitted file has a checkbox (all checked; Space
  toggles), staged files are marked, and **Commit** takes only the checked ones, leaving the rest
  uncommitted. **Amend** puts them into the last commit, keeping its message or with a new one, and
  warns when that commit is already pushed. Right-click a file to leave it out or discard its changes.
- Closing a tab where a command or program is still running, or a connected remote tab, asks first,
  and so does closing the window: one dialog lists what's running and which notes aren't saved, with
  **Save all and close**. Idle tabs close as before. "Don't ask again" (or `[terminal]
confirm_close = false`, also in Settings) stops asking about running things; unsaved notes always
  ask.
- Right-click in a note for editing: undo and redo, cut, copy, paste, select all, find and
  replace, open or copy the link under the pointer, and in Markdown notes bold, italic, code, link,
  headings, bulleted and numbered lists and quotes.
- Blame in the file viewer has three settings, **Off**, **Line** (the current line's author and
  message, the default) and **Gutter** (every line), remembered between files; **B** cycles them.
- **Close tabs to the right** in a tab's right-click menu, next to **Close other tabs**; unsaved
  notes and running commands ask first, as they do there.
- Drag a tab along the tab strip to move it (a marker shows where it lands), or move the current tab
  with Ctrl+Shift+PageUp / PageDown. Ctrl+Tab, Alt+1…9 and the restored session follow the new order.
- The file viewer's line numbers light up under the pointer, the selected lines' numbers stay
  highlighted, and the current line's number is brighter.
- A small git mark next to **Blame** and at the start of the line blame while blame is on.
- Right-click a line number in the file viewer (or one of the selected lines) to copy a link to
  those lines on each remote, at the current commit or on the branch (GitHub, GitLab, Bitbucket,
  Gitea and Codeberg), or to copy the line numbers or `path:line`.
- The note editor edits like a code editor: Ctrl+D adds the next match, Alt+click adds a cursor and
  Alt+drag selects a block; Alt+↑/↓ moves a line, Ctrl+Shift+D duplicates it, Ctrl+Shift+K deletes
  it, Ctrl+L selects it; brackets and quotes close themselves. In Markdown notes Ctrl+B, Ctrl+I and
  Ctrl+K make bold, italic and a link, pasting a URL over selected text makes it a link, and
  Ctrl+Enter ticks a `- [ ]` task. The status line counts words and characters (of the selection when
  there is one).
- **Settings → Privacy** turns off what tk reads beyond your files and tabs: your shell history (alias
  suggestions), Claude Code's logs (usage), and GitHub pull requests in the Git view (`[privacy]` in
  config.toml).
- `tk-app <folder>` opens a tab in that folder, like `code .`: in the app that's already running (it
  comes to the front), or it starts the app with the folder's tab after the restored ones. A
  relative folder starts from where you run it; something that isn't a folder is an error. The .deb
  now installs `tk-app` on your `PATH` too.
- Hover the blame text (the line blame or the gutter) for a moment to see the commit: author and
  email, exact and relative date, hash, the full message, the files it changed with +/− counts and
  its changes to this file, with **Open in Git view**, **Show this file at this commit**, **Copy
  hash** and **Open on the remote**. The card stays while the pointer is on it; Esc or moving away
  closes it.
- Pre-releases: an update channel in **Settings → Updates** (`[updates] channel` in config.toml).
  `stable`, the default, offers releases only; `beta` also offers betas and release candidates
  (0.12.0-beta.1, 0.12.0-rc.1) to try the next version early; `alpha` offers every pre-release.
  Versions now sort by SemVer, so someone on a release candidate is offered its release.

### Changed

- A side pane keeps its width when you switch views: every pane on a side (Explorer, file viewer,
  Git, Monitor…) uses that side's width, 40% of the tab to start, and dragging a divider sets it for
  all of them. Wide mode in the Git view and the Monitor still goes back to it.

### Fixed

- Long menus, such as the Git view's branch list, no longer run past the bottom of the window: a
  menu fits the window and scrolls, and one with many items gets a filter at the top (type to narrow
  it, ↓ to move into the list, Enter for the first match).
- Agent notifications are calmer and right: by
  default tk tells you only when an agent asks for you, by ringing the terminal bell (for Claude Code:
  `claude config set --global preferredNotifChannel terminal_bell`) or sending a desktop
  notification sequence (OSC 9 / OSC 777, shown with its own text). It no longer guesses from CPU use
  unless you choose that in Settings, and the guess now waits for real work followed by a real
  silence. A tab notifies once until you've looked at it, never while you're in it or just typed in
  it, and several at once arrive as one. Settings → Notifications (`[notifications]` in config.toml)
  also turns off the "command finished" notifications.
- Starting tk while it's already running brings the running app to the front instead of starting a
  second one, so two apps no longer overwrite each other's saved tabs.
- Every jump from one side pane to another can go back with ‹: from a blame or a file's history to
  the Git view, back to the file at the same line, scroll and revision; from the Explorer's History
  to the Explorer; from a folder in the viewer or the Monitor to the Explorer, back to where you were.
- The line blame in the file viewer follows the pointer, in a thin grey type that brightens under the
  pointer, without the browser's tooltip. Greys meant to be dim in the Explorer, Git view, Monitor
  and Remote pane now are (a colour they used was never defined).
- On an alpha, beta or rc, What's new shows what that pre-release adds (the changelog's
  `[Unreleased]`) under its version, marked Installed.
- `tk note` exits 0 when the note opens, as `tk view` does; it printed an error and exited 1.
- `tk note` and `tk-app <folder>` no longer log "An object could not be cloned" in the window.
- Enter in the dialog that asks before closing tabs no longer discards unsaved notes: it saves them,
  or, with only running commands listed, keeps the tabs open.
- Closing several tabs asks "Close these tabs?", not "Close this tab?".
- The Git view's branch menu sorts names the way people count: topic-2 before topic-10.
- A Markdown note's right-click menu shows the Bold, Italic and Link shortcuts (Ctrl+B, Ctrl+I,
  Ctrl+K).
- In the file viewer, pressing on a line number selects that line and dragging selects more lines
  (Shift+click extends); it used to select the numbers as text.
- The Git view keeps the commit message you typed until a commit lands, so a commit a hook refuses
  doesn't lose it.
- A link to lines on a remote says "not pushed yet" when the remote doesn't have that commit or
  branch, and the blame card offers **Open on the remote** only for commits that are there.
- The Git view fits a side pane at its starting width: a narrow pane leaves out the Author and Commit
  columns (both in the commit's details) and the title, instead of scrolling sideways and clipping
  the search box; a wider pane or wide mode shows them.
- Clicking past the end of a line in the file viewer no longer jumps to the Git view: the line blame
  follows the pointer, and pressing on it opened the commit. Now Ctrl+click opens it, as links do in
  VS Code; **Settings → File viewer** (`[viewer] blame_click` in config.toml) can make a plain click
  open it instead (like JetBrains' annotations) or nothing (like GitLens, whose hover card has **Open
  in Git view**). Only the left button ever opens it.

## [0.10.2] - 2026-10-16

### Added

- **Processes** in the Monitor: every process on the
  machine, like htop. Sort on any column (CPU, memory, disk, PID, time, threads, user, command; `c`,
  `m` and `p` for the common ones), drag column edges to resize them (double-click to fit), show or
  hide columns from the header's right-click menu, and choose how many rows show (footer or Settings;
  `[monitor] processes` in config.toml). Filter by name, command, PID, `user:root` or `:3000` (what
  listens on a port), or narrow to your processes, a tab's, running ones or zombies. Stop a process
  from its row (one more click to confirm), with Delete (Shift+Delete kills), or right-click for kill,
  stop with its children, pause/resume, other signals, lower priority, its folder in the Explorer or
  a new tab, copy PID or command line, and details (command line, program, folder, parents, ports,
  systemd unit or container, CPU and memory charts). Another user's process offers "Kill with sudo in
  a new tab". The list stays still while the pointer is on it. ⤢ in the Monitor's header widens it
  over most of the tab. `tk monitor --json --procs` prints the same list for scripts and agents.
- The Monitor's **Tabs** section manages processes too: right-click a tab to interrupt its running
  command (Ctrl+C), stop or kill all its processes (the shell stays), open its details, copy its PIDs
  or close it; right-click a process in a tab's tree for the same menu as the Processes list. How many
  processes a tab lists before "Show more" is a setting (`[monitor] tab_processes`).

## [0.10.1] - 2026-10-16

### Fixed

- `rcd` and `repo` completion no longer fills the screen with every folder as an absolute path:
  nothing is listed until you type, then the best ten matches, shown and inserted as `~/…` (so your
  history stays readable too). Picking one and pressing Enter goes there in one step; other commands
  keep Enter's usual behaviour in the menu. A typo while completing no longer rescans every folder,
  and tk's own app data is left out of the folder index.
- Inside full-screen programs (tmux, vim, emacs, htop…), Alt+1…9, Ctrl+PageUp/PageDown, Ctrl+Tab
  and Ctrl+= / - / 0 now reach the program instead of switching tabs or changing the font size. tk's
  Ctrl+Shift shortcuts keep working everywhere.
- **Rename tab** in a tab's right-click menu now renames it, the same as double-clicking the tab.

## [0.10.0] - 2026-10-16

### Added

- Find in a terminal's output: Ctrl+Shift+F (or
  right-click → Find…) opens a find bar over the terminal with a match count, Enter / Shift+Enter
  (and F3) for next / previous, and toggles for match case, whole word and regular expressions. Every
  match is outlined and the current one filled; Esc closes it.
- tk reopens your tabs after a restart, a crash or an update: their order, folders, names and open side panes,
  and note tabs with their files. Remote tabs come back waiting for Enter instead of connecting at
  once. Settings → "Reopen my tabs" (`terminal.restore_tabs`) turns it off.

### Changed

- The Monitor's Tabs section is redesigned. Each tab
  shows what it's doing (running a command and for how long, an agent working or waiting, idle,
  disconnected), the ports it listens on, CPU with a history line, memory against your RAM, disk
  reads and writes, and its process count; columns sort, and a totals row sums them. Opening a tab
  shows CPU and memory history with peaks, disk, scrollback size and threads, and its real process
  tree (with how long each process has run, and Stop).
- Typing shows up without the 5 ms output delay:
  output after a quiet moment is sent at once, while busy output is still batched as before.

## [0.9.3] - 2026-10-15

### Fixed

- A new tab's first prompt no longer shows as if a command had failed: tk's `.zlogin` forwarder left the exit status at 1
  when you have no `~/.zlogin`.

## [0.9.2] - 2026-10-15

### Fixed

- Git view: remote branch labels no longer spill over
  the commits around them (they picked up the Remote pane's layout through a shared class name).
  Long labels shorten with an ellipsis (the full name shows on hover) and leave room for the commit
  message; past two labels, the rest collapse into "+N".
- The first `cd` in a new home folder no longer prints a `chpwd-recent-dirs` error: tk's zsh setup creates the folder
  zsh-autocomplete keeps recent folders in.

### Added

- Git view: column headers (Graph, Description, Author, Date, Commit), and columns you resize by
  dragging a header edge; widths are remembered, and a double-click on the edge resets one.

## [0.9.1] - 2026-10-15

### Changed

- The code is reorganized so it can be maintained.
  Nothing you use changes, except the fixes below.
  - The main process is split into one module per area in `app/main/`; `main.js` only sets
    Electron up and wires them.
  - Tabs are split into tab lifecycle, the terminal, side pane layout and menus, and every keyboard
    shortcut lives in one action registry (`ui/actions.mjs`) that the app menu's shortcut list also
    reads.
  - The Git view's graph layout is plain, tested functions; its menus and the rebase editor have
    their own modules.
  - One dialog component and one set of DOM helpers instead of copies; the CSS is one file per area.
  - Prettier formats the code, ESLint checks it, and JSDoc types are checked in CI.
  - `docs/ARCHITECTURE.md` has a code map: where each feature lives and how to add one.
- Scrollbars are dark and thin everywhere, including the code viewer, notes, dialogs and horizontal
  bars.

### Fixed

- Ctrl+Shift+X, A, E, G and M in a note tab threw an error; they now go to the editor.
- The app menu drew a focus outline around its whole content area when opened from the keyboard.

### Added

- Tests: an end-to-end smoke test that starts the app and walks through tabs, panes, the Git view,
  the viewer, notes, dialogs and shortcuts; unit tests for the git graph and parsers, SSH
  config, containers, secret detection, PATH merging, versions and the shortcut registry; and
  core tests for `tk config set`. All run in CI, and the release workflow runs the smoke test against
  the built package before uploading it.

## [0.9.0] - 2026-10-15

### Added

- App menu: the layers icon in the window's
  top-left corner opens a dialog (Esc or × closes it) with:
  - **Updates**: checks GitHub for a newer release and shows its notes. An AppImage downloads the
    new one, verifies it against `SHA256SUMS`, replaces itself and restarts; a .deb is saved to
    Downloads, verified and opened in Software. A daily check puts a dot on the icon when an update
    is out.
  - **About**: version, release date, package type, component versions and the license.
  - **Settings**: scrollback, theme, plugins, `load_user_zshrc` and rcd's folders as a form, saved to
    `config.toml` with its comments kept. Scrollback applies to open tabs at once.
  - **Keyboard shortcuts**, searchable; **What's new** from the changelog; **Report a problem**,
    which opens a GitHub issue filled in with the app's details.
- `tk config set <key> <value>` changes one setting and keeps the file's comments.

## [0.8.2] - 2026-10-15

### Fixed

- tk used a lot of memory and CPU, and its downloads were large. Measured on the packaged app against 0.8.1:
  - One tab: 308 → 261 MB. Chromium's network service and GPU work now run in the main process
    instead of two more processes (`TK_GPU_PROCESS=1` brings the GPU process back), and CodeMirror
    and the Markdown renderer load when you first open a file or a note.
  - Five tabs with full scrollback: 492 → 402 MB. Tabs keep 5000 lines instead of 10000. Each kept
    line costs memory whether you scroll or not; set `[terminal] scrollback` in `config.toml` to
    change it.
  - A busy TUI redrawing the screen: 47% → 37% of a core. Shell output is sent to the window in
    batches every 5 ms instead of chunk by chunk.
  - AppImage 130 → 100 MB: one locale instead of 55, and no source maps, TypeScript sources or
    node-pty builds for Windows and macOS; the AppImage is compressed harder. The .deb (already
    xz) goes 103 → 100 MB. The rest is Electron itself.

### Added

- `tk config` prints the settings tk is using, with defaults filled in (`--json` for scripts).

## [0.8.1] - 2026-10-15

### Changed

- Thicker lines on the activity bar icons, which were hard to make out.

### Fixed

- Commands installed into `~/.local/bin` (or anywhere your own shell config adds to PATH) were "command
  not found" in tk's tabs. tk's zsh uses its own
  config, so the PATH lines installers write to `~/.zshrc`, `~/.bashrc` or `~/.profile` never ran. tk
  now reads PATH from your login shell (and your own zsh config) once at startup, like VS Code, and its
  zsh also runs your `~/.zprofile` and `~/.zlogin`.

## [0.8.0] - 2026-10-15

### Added

- Shell config sync: **Shell config…** on a host
  or container in the Remote pane brings your tk aliases and dotfiles you pick. On an SSH host tk
  writes `~/.tk/shell.sh` plus one marked line in the remote `.bashrc` / `.zshrc` (Remove undoes
  it); copied dotfiles keep a backup of the one they replace. Containers default to loading your
  aliases in each new shell without writing anything into them. The dialog shows what will change
  first, leaves out lines that look like secrets, and warns about Oh My Zsh or a missing shell.
- `tk alias sh`: your aliases as code for other machines (plain aliases for any `sh`, functions
  with parameters for bash and zsh).
- Oh My Zsh (with its `git` plugin), zsh-autosuggestions, fast-syntax-highlighting and
  zsh-autocomplete ship with tk, pinned in `core/assets/bundle.txt`: `tk shell setup` copies them
  in without git or a network connection, and a newer tk refreshes them. Plugins you installed with
  git keep updating with git. New configs also turn on zsh-autocomplete.
- SSH tabs share one connection per host (`ControlMaster`, kept 10 minutes), which the sync reuses:
  log in once, no second password or 2FA prompt.

## [0.7.0] - 2026-10-15

### Added

- Remote: a Remote pane (Ctrl+Shift+R) with your
  SSH hosts from `~/.ssh/config` (and its `Include`s), recently opened hosts and containers, and
  Docker and Podman containers. Open a terminal on a host or a shell in a container in a new tab,
  marked with the host's colour and shown in the status bar. A remote tab stays open when its
  connection ends and reconnects with Enter. Add a host (appended to `~/.ssh/config`), test a
  connection without prompts, edit the config in a note tab, start and stop containers. Explorer
  and Git are off in remote tabs for now.

### Changed

- Every side pane opens on the right by default (move any of them to the left from the activity
  bar); side choices saved under the old defaults are reset.
- A slimmer activity bar (28px).

## [0.6.0] - 2026-10-15

### Added

- An activity bar on the left edge with the Explorer, Git, Monitor and Aliases buttons, which leave
  the status bar.
- Side panes open on either side of the terminal: one pane per side, so a left and a right pane can
  be open together (for example the Explorer and the file you opened from it). Choose each pane's
  side by right-clicking its button or from the gear; Explorer and Git default to the left, the
  Monitor, Aliases and the file viewer to the right. Each side has its own divider, and widths are
  remembered per pane.

### Changed

- The tab strip starts after the activity bar instead of above it.
- Side panes have a crisp edge toward the terminal, and the Monitor fits its default width without
  scrolling sideways: a tighter Tabs table, and the Claude note wraps instead of widening the pane.

## [0.5.5] - 2026-10-14

### Fixed

- Closing the app while a shell was still printing showed an "Object has been destroyed" error and
  left the app hanging. Output that arrives after
  the window is gone is now dropped.

### Changed

- Monitor pane: a cleaner six-tooth gear icon that follows the theme color.

## [0.5.4] - 2026-10-14

### Added

- Monitor pane: a network graph (download and upload) in System; a gear menu to show or hide each
  section and change their order; sections can be dragged by their header. The layout is remembered.
- Monitor pane: the Tabs section is a table with column headers (tab, activity, CPU, memory,
  processes, busiest process); each tab shows its folder or running command, and its processes
  open in their own headed table.
- A new find bar in the viewer and note tabs: match case, whole word and regex as equal-size toggles
  inside the search box, a "3 of 12" count, previous/next/close, and a collapsible replace row
  (note tabs). The Find button now opens and closes it.

### Changed

- Monitor pane: content keeps its width and scrolls sideways when the pane is too narrow, instead of
  squashing or overlapping (the signed-in line stays on one line).

## [0.5.3] - 2026-10-14

### Changed

- `docs/READINESS.md`: a new gap, **18. Polish and product feel**: a design system with shared components, one
  keyboard model, a quality bar for every pane (empty, loading and error states, first use, keyboard,
  narrow windows, large data, failures), a first-run experience, consistent confirmation and undo
  for destructive actions, and a week of dogfooding. Gap 14 now names the core workflows and a
  feature freeze; the suggested order puts gap 18 right after the P0 gaps.

## [0.5.2] - 2026-10-14

### Changed

- `docs/READINESS.md` shows where each gap stands: a status and issue column in the summary, what
  v0.5.1 finished for the sandbox, packaging and CI gaps and what is left, and a list of smaller
  open points (follow-ups, checks that need a real desktop, features not yet exercised for real).

## [0.5.1] - 2026-10-14

Packages and releases.

### Added

- Release packages built by GitHub Actions for every tag and attached to its release: an AppImage, a
  .deb, the `tk` binary on its own, `SHA256SUMS`, and `latest-linux.yml` for auto-update later.
- The .deb installs to `/opt/tk`, sets up Chromium's sandbox (setuid `chrome-sandbox` and an
  AppArmor profile for Ubuntu 24.04+), links `/usr/bin/tk`, and removes all of it on uninstall.
- The app checks at startup whether Chromium's sandbox can work and turns it off only when it can't
  (an AppImage on Ubuntu 24.04+, or a development build without `make apparmor`); the status bar
  then shows **Sandbox off** with the reason.
- CI on every push and pull request: Rust formatting, clippy and tests, and a syntax check of the app.
- Release pages for every earlier version, with notes from this changelog.

### Fixed

- Packaged builds were missing `git.js` (the Git view's backend).
- An empty back button showed in the Git view's header.

## [0.5.0] - 2026-10-14

Monitoring, note tabs, and fixes.

### Added

- **Monitoring**.
  - Status bar along the bottom: the active tab's branch, folder and running command (with a
    timer), the tab's CPU and memory, system CPU, RAM and GPU, and Claude tokens in the current
    usage window with the time until it resets. Items turn yellow or red when usage is high;
    clicking one opens the Monitor pane on that section.
  - Monitor pane (Ctrl+Shift+M, right-click → Monitor): CPU and memory with two-minute graphs,
    per-core load, swap, load average, disk and network rates; every GPU found (NVIDIA through
    nvidia-smi, AMD through sysfs, Intel estimated from the clock speed); each tab's process tree
    with Stop; Claude Code usage: account, current window (input, output, cache), comparison with
    your busiest window, today by model, and this week's sessions linked to their tabs.
  - Notifications when a command of 10 s or more finishes, or an agent (claude, codex, gemini,
    aider, kiro) goes quiet, in a tab you aren't looking at.
  - `tk monitor --json [--watch] [--pids …]` and `tk usage [--json]` in the core.
- **Note tabs** (Ctrl+Shift+N, right-click + → New note, `note [file]`, Explorer → Edit as note): a
  gedit-like editor with syntax highlighting, line numbers, undo, find and replace, wrap and a
  line/column status. New notes save themselves to `~/.local/share/tk/notes/` and take their first
  line as the tab name; files save with Ctrl+S (Save as with Ctrl+Shift+S) and ask before closing
  with unsaved changes. Open lists recent notes.
- Status bar buttons for the Explorer, Git, Monitor and Aliases panes (highlighted while open).
- Git view: drag handles resize the commit details (bottom edge), the commit message, and the split
  between the file list and the diff, for long file names. Sizes are remembered.
- Git view: file history opened from the viewer has a ‹ button back to the file.

### Changed

- Completion: the first Tab completes and lists the choices, the second Tab enters the menu to pick
  one with the arrow keys (zsh's `LIST_AMBIGUOUS` is off). Before, picking needed a third Tab.
- Commit details in the Git view span the full width, so graph lines no longer run down their side.
- The status bar is taller (26 px) with larger, narrower text, and square corners.
- File history in the Git view leaves out redundant lines to ancestors.

## [0.4.1] - 2026-10-14

### Changed

- A VS Code-like look for the Explorer, the Git view, the viewer's toolbar and the alias builder: dense 22–24px rows with flat highlights, small
  uppercase section titles, hairline separators instead of rounded cards, small flat branch and
  tag labels, file names coloured by git status, author names without avatars, and the command
  bar docked to the bottom edge.

## [0.4.0] - 2026-10-14

Git view and code viewer.

### Added

- **Git view** (Ctrl+Shift+G, right-click → Git): a commit graph of the tab's repository with
  branches, tags, remotes, stashes, ahead/behind counts against upstream, and pull requests with
  their check status (through `gh`). Click a commit for its files and diffs inline. Right-click
  for checkout, branch, tag, cherry-pick, revert, merge, rebase, reset, push, pull, PR, rename,
  delete, and stash apply/pop/drop. Every action shows its `git` command and runs it in the tab's
  terminal; the view refreshes at the next prompt.
- Compare any two commits or branches (commits only on each side, the files and diffs between them).
- File history: the graph narrowed to commits that touched a file, following renames.
- Interactive rebase editor: reorder by dragging, pick/reword/squash/fixup/drop, result preview;
  tk hands git the plan, so no editor opens.
- Commit search by message, author, file, or changed text (`git log -S`); `#123` links to GitHub.
- **Code viewer**: files open in a read-only CodeMirror editor with syntax highlighting, folding,
  find (Ctrl+F), go to line (Ctrl+G) and wrap (W). Git in the viewer: change bars against the last
  commit (click to see the replaced lines), blame for the current line, a blame gutter with a
  heatmap (B), changes since the last commit (D), and older versions of the file (‹ ›).
- Markdown shows rendered, with a Source toggle.
- Explorer: right-click a file → Blame or File history.

### Changed

- The app build bundles CodeMirror into `app/vendor/codemirror.mjs` (`npm run vendor`, run by `make`).

## [0.3.1] - 2026-10-14

Follow-ups to the Explorer.

### Added

- Tabs are named after the shell's folder (`~` for home) instead of the whole path, with the full
  path as a tooltip. Double-click a tab (or right-click → Rename tab) to give it a name; right-click
  also offers Use folder name, New tab here, Close tab and Close other tabs.
- **Recent folders** (right-click in the terminal, or the clock button in the Explorer): the folders this tab's
  shell has been in, then the ones you use most; click to jump there (a busy shell gets a new tab).
- Explorer back/forward (‹ ›, Alt+← / Alt+→, mouse back/forward buttons) through the folders it showed.
- Explorer details: lines added/removed next to changed files (`+12 −3`), item counts on folders,
  and a details bar for the selected entry plus a card on hover (type, size, line count, last
  commit, exact date, permissions, owner, symlink target). Both can be turned off in **⋯**.

### Changed

- Choosing Explorer (right-click menu, Ctrl+Shift+E in the terminal, `view`) when it is already
  open brings it back to the shell's folder instead of closing it. Ctrl+Shift+E inside the
  Explorer still closes it.
- Tabs are wider (220 px instead of shrinking to their text).
- The GitHub account was renamed: links and package metadata point at `guidona/tk`.
- The app's interface uses Ubuntu Sans and Ubuntu Sans Mono (falling back to the previous fonts),
  and the Explorer uses one font throughout instead of mixing in monospace.

## [0.3.0] - 2026-10-14

### Added

- **Explorer** in the side pane, replacing the flat folder view.
  A file tree that follows the shell as you `cd` (or stays pinned), with a breadcrumb, git branch
  and change count, per-file git status, dimmed ignored files, type icons, age and size. Fuzzy
  filter (`/`) below the current folder, keyboard navigation, and a right-click menu: Jump in
  here, Open as root, Open in new tab, View, Open with default app, Copy path, Copy relative path,
  Insert into command line, Reveal in file manager. Ctrl+Shift+E, right-click → Explorer, or
  `view <folder>`.
- Files opened from the Explorer show in the viewer with a **‹ Explorer** button (and Esc) to go back.

### Changed

- Context menus leave a small gap between items, so hover highlights don't touch.

## [0.2.1] - 2026-10-14

### Fixed

- Ctrl+Shift+V pasted the clipboard twice in the app: Chromium's own "paste as plain text" ran
  as well as tk's shortcut.

## [0.2.0] - 2026-10-14

### Added

- **Alias builder** in the app's side pane (Ctrl+Shift+A, `aliases`, or right-click a command →
  _Save as alias…_). Click words of a command to make them parameters; set required/optional,
  defaults, order and Tab completion (list, files, or a command's output); preview example calls
  and the generated zsh; try the alias in the tab before saving.
- Aliases are stored in `~/.config/tk/aliases.toml` and become zsh aliases or functions.
  Parameters can be given by position or as `--name value`; unknown flags pass through. Changes
  reach every open shell before its next command.
- `mkalias [name]` saves the last command; `aliases` opens the builder (or lists aliases outside
  the app).
- `tk alias` commands: `add`, `rm`, `list`, `export`, `import` (file, URL or stdin), `suggest`,
  `history`, `zsh`.
- Suggestions for long commands you run often, read from your zsh history.
- The shell marks prompts and commands with an OSC sequence so the app knows which lines belong to
  which command.

## [0.1.0] - 2026-10-13

First version.

### Added

- **Core (`tk` binary, Rust)**
  - `rcd` / `repo`: fuzzy folder and git-repository jumping, with an index of the configured roots,
    frecency ranking, an inline picker for ambiguous matches, and fuzzy zsh tab completion.
  - `tk index`: fast parallel folder scan; refreshes in the background when older than 6 hours, and
    rescans automatically when a query finds nothing.
  - `tk shell setup`: installs Oh My Zsh and known third-party plugins under `~/.config/tk/`, and
    generates tk's own `.zshrc` from `config.toml`. Never modifies `~/.zshrc`.
  - `tk init zsh`: shell integration (`rcd`, `repo`, `view`, `tree`, frecency `cd` hook, completion, and
    the silent-cd widget).
  - `tk view`: asks the running app to show a file or folder.
  - `tk tree`: built-in GNU tree replacement (`-L`, `-a`, `-d`, `-I`, `--noreport`). The shell's
    `tree` uses it unless GNU tree is installed, so `tree` works out of the box.
  - `tk describe [--json]`: machine-readable command list.
  - `~/.config/tk/config.toml` with `[rcd]` roots/excludes and `[shell]` theme/plugins.
- **App (Electron + xterm.js)**
  - Frameless window with tabs, window controls and a Catppuccin-based theme. New tabs open in the
    current tab's folder.
  - Detection of files, folders and URLs in terminal output, with a right-click menu (View, Open with
    default app, Jump in here, Open in new tab, Open in file manager, Copy path/link, Copy, Paste,
    Select all, Clear) and Ctrl+click to open.
  - View pane for markdown (sanitized), images, video, audio, PDF, CSV/TSV, JSON, code/text and
    folders, with a draggable divider.
  - "Jump in here": silent `cd` through a zsh widget, with no command typed and no history entry.
    Disabled while a program is running in the tab.
  - Control socket (`$XDG_RUNTIME_DIR/tk-app-<pid>.sock`) for shell commands such as `view`.
  - Keyboard shortcuts for tabs, copy/paste, the view pane and font size.
  - App icon (SVG masters, PNGs 16–512 px), `tk-app` launcher and app-menu entry (`make desktop`).
- Licensed under Apache-2.0.
- Default look ported from the previous toolkit: **Powerlevel10k** (lean, ASCII mode so any font
  works, one line, sparse, transient and instant prompt), installed by tk, with its config at
  `~/.config/tk/p10k.zsh` (`p10k configure` writes there).
- Default plugins: `git`, `gitignore`, `git-auto-fetch`, `zsh-autosuggestions`, `zsh-completions`
  and `fast-syntax-highlighting`. tk enforces a single syntax highlighter; `zsh-autocomplete` (opt-in)
  loads last and is cloned at its newest release tag. `git-prompt` is supported for other themes.

### Known limitations

- Relative paths in old output are resolved against the shell's _current_ folder.
- The app needs `make apparmor` (or runs with `--no-sandbox`) on Ubuntu 24.04+.
- AppImage packaging is configured but not yet tested.

[Unreleased]: https://github.com/guidona/tk-releases/releases
[0.14.0]: https://github.com/guidona/tk-releases/releases/tag/v0.14.0
[0.12.0]: https://github.com/guidona/tk-releases/releases/tag/v0.12.0
[0.11.0]: https://github.com/guidona/tk-releases/releases/tag/v0.11.0
[0.10.2]: https://github.com/guidona/tk-releases/releases/tag/v0.10.2
[0.10.1]: https://github.com/guidona/tk-releases/releases/tag/v0.10.1
[0.10.0]: https://github.com/guidona/tk-releases/releases/tag/v0.10.0
[0.9.3]: https://github.com/guidona/tk-releases/releases/tag/v0.9.3
[0.9.2]: https://github.com/guidona/tk-releases/releases/tag/v0.9.2
[0.9.1]: https://github.com/guidona/tk-releases/releases/tag/v0.9.1
[0.9.0]: https://github.com/guidona/tk-releases/releases/tag/v0.9.0
[0.8.2]: https://github.com/guidona/tk-releases/releases/tag/v0.8.2
[0.8.1]: https://github.com/guidona/tk-releases/releases/tag/v0.8.1
[0.8.0]: https://github.com/guidona/tk-releases/releases/tag/v0.8.0
[0.7.0]: https://github.com/guidona/tk-releases/releases/tag/v0.7.0
[0.6.0]: https://github.com/guidona/tk-releases/releases/tag/v0.6.0
[0.5.5]: https://github.com/guidona/tk-releases/releases/tag/v0.5.5
[0.5.4]: https://github.com/guidona/tk-releases/releases/tag/v0.5.4
[0.5.3]: https://github.com/guidona/tk-releases/releases/tag/v0.5.3
[0.5.2]: https://github.com/guidona/tk-releases/releases/tag/v0.5.2
[0.5.1]: https://github.com/guidona/tk-releases/releases/tag/v0.5.1
[0.5.0]: https://github.com/guidona/tk-releases/releases/tag/v0.5.0
[0.4.1]: https://github.com/guidona/tk-releases/releases/tag/v0.4.1
[0.4.0]: https://github.com/guidona/tk-releases/releases/tag/v0.4.0
[0.3.1]: https://github.com/guidona/tk-releases/releases/tag/v0.3.1
[0.3.0]: https://github.com/guidona/tk-releases/releases/tag/v0.3.0
[0.2.1]: https://github.com/guidona/tk-releases/releases/tag/v0.2.1
[0.2.0]: https://github.com/guidona/tk-releases/releases/tag/v0.2.0
[0.1.0]: https://github.com/guidona/tk-releases/releases/tag/v0.1.0

# Omarchy Sync Mesh

`lfdm85.omarchy-sync-mesh` is an Omarchy bar widget that keeps portable Omarchy
configuration aligned across machines through a private Git repository. It
syncs plugins, themes, shortcuts, shell settings, supported application
profiles, terminal settings, hooks, and helper scripts.

## Install

```bash
omarchy plugin add https://github.com/LFDM-85/omarchy-sync-mesh.git --enable --yes
```

The widget is placed on the right side of the bar by default. Move it at any
time with Omarchy's bar controls.

```bash
omarchy bar move lfdm85.omarchy-sync-mesh --section left
```

## First use

Click the Sync Mesh icon and paste the URL of a **private** GitHub repository
that will contain your Omarchy profile. The plugin always asks for this URL;
it never assumes a repository.

- On the source machine, select **Send this machine**. It captures the
  portable profile, commits it, and pushes it to your private repo.
- On another machine, install the plugin, enter the same repo URL, then select
  **Receive from repo**. A timestamped backup is created before incoming files
  are applied.
- Use **Choose** to inspect changes and decide what to keep when both the
  machine and repository changed the same configuration.

Display layout is machine-specific by default. It is only applied when you
explicitly opt in.

For the full setup, authentication and recovery walkthrough, see
[GETTING-STARTED.md](GETTING-STARTED.md). Use **Send this machine** on the
source, then **Receive from repo** on the destination. Review is required if
the destination already has local changes. The app lists are captured, but
installing applications is a separate action in the panel.

## What it syncs

- Hyprland shortcuts and portable configuration
- Omarchy shell settings, all user themes including images, hooks, extensions,
  and branding; the selected theme is applied when available
- Portable local plugins (excluding Sync Mesh itself)
- AI Markdown: top-level `.md` files and Markdown under `skills/`, `agents/`,
  `commands/`, `rules/` and `memories/` in `~/.claude`, `~/.codex`,
  `~/.agents`, `~/.gemini` and `~/.hermes`. These are stored under `ai/` in
  the profile and restored to their original directories.
- Terminal configuration and local helper scripts
- Installed application manifests for a new-machine bootstrap

Git credentials are handled by your existing SSH setup or Git credential
helper. The widget never requests or stores a GitHub password.

Markdown instructions can contain private information or secrets. Review the
profile before publishing; the plugin does not scan contents for secrets. Use a
private repository. Sessions, plans, non-Markdown AI settings, symlinks and
project-specific files outside the listed directories are not included. Files
over 50 MiB are skipped; the local profile clone has a 2 GiB limit and each operation has a 512 MiB limit.
Monitor layouts are excluded by default. Plugins and AI instructions can run
or direct code: only apply profiles you trust.

## Removal

```bash
omarchy plugin remove lfdm85.omarchy-sync-mesh --yes
```

Removal deletes only the installed widget and its Sync Mesh state. It does not
delete your configuration repository or any local configuration files.

## Development

```bash
omarchy plugin validate .
python3 -m unittest discover -s tests -q
```

This project builds on original work by Dmytro Gladkyi and remains available
under the MIT license. See [LICENSE](LICENSE).

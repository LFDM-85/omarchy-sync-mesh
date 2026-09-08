# Omarchy Sync Mesh

`lfdm85.omarchy-sync-mesh` is an Omarchy bar widget that keeps portable Omarchy
configuration aligned across machines through a private Git repository. It
syncs plugins, themes, shortcuts, shell settings, supported application
profiles, terminal settings, hooks, and helper scripts.

## Install

```bash
omarchy plugin add https://github.com/LFDM-85/omarchy-sync-mesh.git --enable
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

- On the source machine, select **Publish this machine**. It captures the
  portable profile, commits it, and pushes it to your private repo.
- On another machine, install the plugin, enter the same repo URL, then select
  **Refresh & Apply**. A timestamped backup is created before incoming files
  are applied.
- Use **Choose** to inspect changes and decide what to keep when both the
  machine and repository changed the same configuration.

Display layout is machine-specific by default. It is only applied when you
explicitly opt in.

## What it syncs

- Hyprland shortcuts and portable configuration
- Omarchy shell settings, themes, hooks, extensions, and branding
- Portable local plugins (excluding Sync Mesh itself)
- Terminal configuration and local helper scripts
- Installed application manifests for a new-machine bootstrap

Git credentials are handled by your existing SSH setup or Git credential
helper. The widget never requests or stores a GitHub password.

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

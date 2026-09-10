# niri-audit

Small, dependency-light CLI tools for inspecting and maintaining a Fedora desktop running Niri.

## Features

- Interactive terminal menu with `niri-audit`
- Health, service, log, config-diff, snapshot, and restart commands
- Read-only system snapshot for versions, units, checksums, outputs, warnings, and available updates
- Optional daily systemd timer
- Optional integrations documented below, kept outside the core repository

## Install

```bash
install -Dm755 bin/niri-audit ~/.local/bin/niri-audit
install -Dm755 bin/niri-system-audit ~/.local/bin/niri-system-audit
install -Dm755 bin/niri-audit ~/.local/bin/niri-audit
install -Dm755 bin/niri-system-audit ~/.local/bin/niri-system-audit
```

Run manually with `niri-audit`. Enable the optional daily timer with:

```bash
systemctl --user enable --now niri-system-audit.timer
```

## Commands

```text
niri-audit                 interactive menu
niri-audit health          versions and failed units
niri-audit services        relevant user services
niri-audit logs            recent relevant warnings
niri-audit configs         active/tracked config differences
niri-audit audit           generate a snapshot
niri-audit snapshot        view the snapshot
niri-audit restart waybar  restart a safe component
```

The snapshot is written to `~/.local/state/niri-fedora-system/system-snapshot.md`.

This public core version intentionally does not include Codex skill-update automation; that workflow is specific to an individual local installation.

## Optional local integrations

The repository intentionally excludes machine-specific integrations such as Brave extensions, raw-input gesture services, and systemd unit files. Add those locally under your own configuration directories if needed; do not commit browser profiles, logs, private configs, or credentials.

For a Brave carousel integration, use an unpacked extension under `~/.config/brave/` and load it from `brave://extensions`. If a raw-input helper uses `libinput` and `ydotool`, keep its device paths and user service files local to the machine.

## Scope and privacy

The audit is read-only apart from its own snapshot. It does not upload data. Review generated snapshots before sharing them: package names, device paths, output names, and local paths may identify your machine. Do not publish personal configs, browser profiles, logs, credentials, or private keys.

## License

MIT. See `LICENSE`.

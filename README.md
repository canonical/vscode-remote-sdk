# VS Code Remote Development SDK for Workshop

This SDK enables VS Code Remote Development over SSH in a workshop. It
configures the SSH server for passwordless access, so VS Code can connect to
the workshop as a remote host. The `.vscode-server` directory is persisted on
the host to preserve extensions and settings across workshop updates.

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: vscode-remote-env
base: ubuntu@24.04
sdks:
  - name: vscode-remote
    channel: latest/stable
```

This creates a workshop that accepts VS Code Remote SSH connections.
After launch, open VS Code on the host, use **Remote-SSH: Connect to Host**,
and enter `workshop@<ip>`.

---

## Using the SDK

### Connect from VS Code

Once the workshop is ready, find the workshop's bridge IP:

```bash
workshop exec <name> -- ip a
```

Then in VS Code on the host:

1. Install the
   [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
   extension.
2. Open the Command Palette and select **Remote-SSH: Connect to Host**.
3. Enter `workshop@<ip>` where `<ip>` is the workshop's IP address.

Alternatively, from a terminal:

```bash
code --folder-uri vscode-remote://ssh-remote+workshop@<ip>/project
```

---

## Plugs (resources this SDK consumes)

### `vscode-server`

- Interface: `mount`
- Workshop target: `/home/workshop/.vscode-server`
- Mode: `0o700`
- Purpose: Persists VS Code Server extensions, settings, and cached data
  between workshop updates. On first connection, VS Code downloads its server
  component into this directory; the mount ensures it survives across workshop
  updates.

## Slots (resources this SDK provides)

This SDK doesn't define any slots.

---

## Documentation and guidance

- [VS Code Remote Development documentation](https://code.visualstudio.com/docs/remote/remote-overview)
- [Remote - SSH extension](https://code.visualstudio.com/docs/remote/ssh)
- [Workshop documentation](https://canonical-workshop.readthedocs-hosted.com/latest/)

---

## Community and support

- VS Code community:
  [VS Code GitHub Discussions](https://github.com/microsoft/vscode/discussions)
- Workshop forum:
  [Workshop Discourse](https://discourse.canonical.com/c/engineering/workshops/34)
- Please review our
  [Code of Conduct](https://ubuntu.com/community/ethos/code-of-conduct) before
  participating.

---

## Contributions

All contributions, including code, documentation updates, and issue reports,
are welcome!

- See `CONTRIBUTING.md` for guidelines.
- Open issues or pull requests on the official repository.

---

## License and copyright

Copyright 2026 Canonical Ltd.

This program is free software: you can redistribute it and/or modify it under
the terms of the
[GNU General Public License version 3 (GPLv3)](https://www.gnu.org/licenses/gpl-3.0.html)
as published by the Free Software Foundation.

[VS Code](https://github.com/microsoft/vscode) is licensed under the
[MIT License](https://opensource.org/licenses/MIT).

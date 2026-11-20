# hub — Fyso extension

Connects a project to the **Fyso hub** of its host: the panel's top bar gets a menu
beside the project name that jumps to the other instances' panels, and the Apps screen
gets a tile back to the hub's entry page.

```bash
mise run ext:add hub                       # asks for the hub's address
mise run ext:add hub -- -d hub_url=https://portal.example.com
```

## What it adds

| Slot | Content |
|---|---|
| `extensions/hub/switcher.yaml` | `url: <hub_url>/environments.json` ([contract §9](https://github.com/fyso-dev/agentic-framework/blob/preview/docs/extensions-contract.md#instance-switcher-panel-api-3)) |
| `extensions/hub/app.yaml` | Tile to `<hub_url>/` |

No process, port, secret or workflow.

## Requirements

- Fyso Agentic Framework v0.1.2 or later (panel API 3); Copier refuses an older one.
- A hub that serves `/environments.json` to its projects' panel origins with CORS (fyso-hub
  with the instance switcher). The hub decides who sees which instance: each person gets
  only the environments whose `allow` list includes them. Without it the menu simply
  does not appear.

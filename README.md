# omarchy-session-actions-power

A drop-in replacement for the stock [Omarchy](https://omarchy.org/) power/battery
bar widget that adds a row of session-action buttons below the power-profile
picker.

Five icon-only buttons, separated from the profile picker by a divider, each
showing its name on hover:

| Icon | Action | Command |
|---|---|---|
| 🔒 | Lock | `omarchy-system-lock` |
| power-sleep | Sleep | `systemctl suspend` |
| restart | Restart | `omarchy-system-reboot` |
| power | Shutdown | `omarchy-system-shutdown` |
| 💀 | Kill | `pkexec systemctl poweroff --force --force` |

Lock/Sleep/Restart/Shutdown match what Omarchy's own command menu already
runs for those actions. **Kill is different on purpose**: it's an immediate,
unconfirmed hard power-off — no orderly shutdown, nothing synced or unmounted
first, closer to pulling the plug than a normal shutdown. It needs root
(`CAP_SYS_BOOT`), hence `pkexec` — this is a bar-panel button with no
terminal to type a `sudo` password into, so expect a polkit prompt on first
use unless you already have passwordless poweroff configured.

The skull icon and the theme's urgent/danger color mark the Kill button apart
from the other four at a glance. That's the only safeguard — there is no
confirmation dialog, by design. If you don't want a single mis-click to
hard-power-off your machine, don't install this, or remove the Kill button
from `Panel.qml` before you do.

Everything else — battery stats, charge info, power-profile picker — behaves
exactly like the stock panel, since this is a clone of it with one row added.

## Install

```
omarchy plugin add https://github.com/Thomster/omarchy-session-actions-power.git
```

Installing switches the bar's power widget over to this plugin in place of
the stock one.

## Requirements

- `polkit` for the Kill button's `pkexec` prompt (standard on any Omarchy
  install)

## License

MIT

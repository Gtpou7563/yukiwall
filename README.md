# yukiwall

**yukiwall** is a lightweight firewall frontend for **nftables**, designed to simplify management of Linux firewall rules while maintaining full control and safety.

---

## Features

* Add or remove rules: `allow`, `block`, `delete/remove`
* Filter by source IP or subnet: `from <ip/subnet>`
* Filter specific ports and protocols: `to <ports>` (tcp/udp/both)
* List rules with unique IDs: `list`
* Reload rules immediately: `reload`
* Flush all rules: `flush`
* Manage logging for unmatched or invalid packets: `logging unm|inv on|off`
* Set policy for invalid packets: `invalid drop|allow`
* View current firewall status: `status`
* Fully compatible with **nftables**
* Compatible with tools (e.g., Docker) that use their own nftables tables or chains.

---

## Requirements

* Python 3.xx
* Root privileges for firewall modifications
* Dependencies (installed automatically via `install.sh`)

---

## Installation

Clone and install:

```bash
cd $HOME && git clone https://github.com/mintyYuki/yukiwall.git && cd yukiwall && sudo bash install.sh
```

### Updating

```bash
cd $HOME/yukiwall && sudo bash update.sh
```

### Uninstall

```bash
cd $HOME/yukiwall && sudo bash uninstall.sh
```

---

## Usage

```bash
sudo yukiwall <command> [args...]
```

---

### Commands

| Command             | Options / Syntax              | Description                                                        |
| ------------------- | ----------------------------- | ------------------------------------------------------------------ |
| `allow from`        | `<ip/subnet> [to <ports>]`    | Allow traffic from a source IP/subnet, optionally to certain ports |
| `allow to`          | `<ports>`                     | Allow traffic to specified ports globally                          |
| `block from`        | `<ip/subnet>`                 | Block traffic from a specific source                               |
| `delete` / `remove` | `id, range, list, or literal` | Remove rules by ID, range, list, or by specifying rule content     |
| `list`              | —                             | List all current rules with their IDs                              |
| `reload`            | —                             | Reload rules without restarting the service                        |
| `flush`             | —                             | Remove all rules (resets to default drop)                          |
| `logging`           | `on` / `off`                  | Enable or disable logging for unmatched and invalid packets        |
| `logging unm`       | `on` / `off`                  | Enable or disable logging for unmatched packets                    |
| `logging inv`       | `on` / `off`                  | Enable or disable logging for invalid packets                      |
| `invalid`           | `drop` / `allow`              | Set default action for invalid packets                             |
| `status`            | —                             | Show current firewall status and configuration consistency         |

---

### Examples

* Allow SSH from a local network:

```bash
sudo yukiwall allow from 192.168.0.0/16 to tcp/22
```

* Allow HTTP and HTTPS globally:

```bash
sudo yukiwall allow to tcp/80,tcp/443
```

* Block a specific subnet:

```bash
sudo yukiwall block from 10.0.0.0/24
```

* Remove rules by ID or range:

```bash
sudo yukiwall delete 3
sudo yukiwall delete 1-5
sudo yukiwall delete 1,3,7
```

* Remove a rule by content:

```bash
sudo yukiwall delete allow to tcp/80
```

* List current rules:

```bash
sudo yukiwall list
```

* Enable logging for all dropped packets:

```bash
sudo yukiwall logging on
```

* Disable logging for unmatched packets only:

```bash
sudo yukiwall logging unm off
```

* Drop invalid packets:

```bash
sudo yukiwall invalid drop
```

* Flush all rules:

```bash
sudo yukiwall flush
```

* Check firewall status:

```bash
sudo yukiwall status
```

---

## How it works

1. Stores rules in `/etc/yukiwall.json`.
2. Generates a consistent **nftables** configuration based on rules.
3. Applies rules via `nft` and ensures the `nftables` service is active.
4. Optional logging for unmatched or invalid packets.
5. Prevents duplicate or unsafe rules.

> ⚠ **Remote SSH Warning:** Ensure your SSH port is allowed before applying rules remotely. Yukiwall will not automatically preserve access.

---

## Notes and Limitations

* New project; some issues may exist.
* Report issues and contribute on GitHub for improvements.

---

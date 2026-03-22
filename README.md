# 🌸 yukiwall

**yukiwall** is a super tiny, ultra-cute firewall frontend for **nftables**, the modern and recommended Linux firewall backend.

---

## ✨ Features

* Interactive port setup: `configure`
* Add or remove allowed ports on the fly: `add` / `remove`
* Peek at your current ports: `list`
* Turn firewall on or off: `enable` / `disable`
* Powered by **nftables** - modern, clean, and efficient

---

## 💻 Requirements

* Python 3.xx
* Dependencies (handled automatically by `install.sh`)
* Root privileges for firewall changes

---

## 🚀 Installation

Clone and install in one line:

```bash
cd $HOME && git clone https://github.com/mintyYuki/yukiwall.git && cd yukiwall && sudo bash install.sh
```

### 🔄 Updating

```bash
cd $HOME/yukiwall && sudo bash update.sh
```

### ❌ Uninstall

```bash
cd $HOME/yukiwall && sudo bash uninstall.sh
```

---

## 🛠 Usage

```bash
sudo yukiwall <configure|add|remove|list|enable|disable>
```

### Examples

* Configure interactively:

```bash
sudo yukiwall configure
```

* Add ports:

```bash
sudo yukiwall add tcp/80 udp/53 both/443
```

* Remove ports:

```bash
sudo yukiwall remove tcp/22
```

* List allowed ports:

```bash
sudo yukiwall list
```

* Enable firewall:

```bash
sudo yukiwall enable
```

* Disable firewall:

```bash
sudo yukiwall disable
```

> ⚠️ **SSH Warning:** yukiwall will warn you if port 22 isn't allowed, so you don't get locked out <3

---

## 🧩 How it works

yukiwall keeps it simple:

1. Saves allowed ports to `/etc/yukiwall.json`
2. Generates a clean **nftables** config
3. Applies it via `nft` and keeps the service running

All the heavy lifting is handled by the backend — you just choose which ports are allowed ✨

---

## 🐛 Caveats

* **Fresh project:** there might be some bugs;
* Please open an issue on GitHub if you run into trouble;
* Over time, it’ll get even better.

---

Made with love by **yuki**, for those who are tired of bugs and complexity.

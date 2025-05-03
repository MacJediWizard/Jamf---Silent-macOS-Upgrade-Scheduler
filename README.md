# Jamf Silent macOS Upgrade Scheduler

A silent macOS upgrade orchestration wrapper for [Graham Pugh's erase-install](https://github.com/grahampugh/erase-install),  
designed for enterprise environments using Jamf Pro or other MDMs.

This script silently pre-caches macOS installers and prompts users only at the final decision point, balancing user flexibility with enforced upgrade deadlines.  
Now with **automatic dependency installation**, **snooze functionality**, **login-time installation**, and **comprehensive diagnostics**.

---

## Features

- 🚀 Silent installer download and caching
- 🛡 Minimal user interruption
- ⏳ 24-hour deferral support (up to 3 times)
- ⏰ Snooze option for short-term deferrals (1-4 hours)
- 🔒 Forced upgrade after 72 hours or 3 deferrals
- 📅 Flexible scheduling options (today, tomorrow, or at next login)
- 🔐 Lock file mechanism to prevent multiple simultaneous executions
- 🎯 Enhanced UI handling with proper user context display
- 🛠 Full dry-run testing with erase-install's `--test-run`
- 📦 Auto-installs erase-install and swiftDialog if missing
- ✍️ Configurable dialog text, button labels, and window position
- 🔄 Robust process tracking and cleanup procedures
- 📊 Comprehensive system diagnostics for troubleshooting
- ✅ Enterprise-grade error handling, structured logging (INFO/WARN/ERROR/DEBUG)

---

## Requirements

- macOS 11 or newer
- [erase-install](https://github.com/grahampugh/erase-install) v37.0 or later
- [swiftDialog](https://github.com/bartreardon/swiftDialog) installed on client Macs
- (Optionally: Jamf Pro to manage deployment)

---

## Configuration

At the top of the script, these options are configurable:

| Variable | Purpose | Default |
|:---------|:--------|:--------|
| `INSTALLER_OS` | Target macOS version to upgrade to | `15` |
| `MAX_DEFERS` | Maximum allowed 24-hour deferrals | `3` |
| `TEST_MODE` | Enable dry-run testing mode | `false` |
| `AUTO_INSTALL_DEPENDENCIES` | Auto-install erase-install and swiftDialog | `true` |
| `DEBUG_MODE` | Enable verbose debug logs | `false` |
| `ENABLE_SNOOZE` | Enable short-term snooze option | `true` |
| `SNOOZE_HOURS` | Hours to snooze when option selected | `4` |
| `ENABLE_LOGIN_SCHEDULING` | Allow scheduling at next login | `true` |
| `DIAGNOSTICS_ENABLED` | Enable system diagnostics reporting | `true` |
| `DIALOG_TITLE` | Dialog window title text | `"macOS Upgrade Required"` |
| `DIALOG_MESSAGE` | Dialog main message | `"Please install macOS $INSTALLER_OS."` |
| `DIALOG_INSTALL_NOW_TEXT` | Text for 'Install Now' button | `"Install Now"` |
| `DIALOG_SCHEDULE_TODAY_TEXT` | Text for 'Schedule Today' button | `"Schedule Today"` |
| `DIALOG_DEFER_TEXT` | Text for 'Defer 24 Hours' button | `"Defer 24 Hours"` |
| `DIALOG_ICON` | Dialog window icon (SF Symbol or path) | `"SF=gear"` |
| `DIALOG_POSITION` | Dialog window screen position | `"topright"` |

---

## Usage

1. Deploy the script to client Macs via Jamf Pro or another MDM.
2. Ensure erase-install and swiftDialog are either installed or allow the script to auto-install them.
3. Customize top-of-script variables as needed (macOS version, dialog texts, etc).
4. Launch the script manually, via Jamf policy, or a LaunchDaemon trigger.

---

## Scheduling Options

The script now provides multiple scheduling options:

- **Install Now**: Begins installation immediately
- **Schedule Today**: Allows selecting a time later today 
- **Defer 24 Hours**: Postpones for 24 hours (up to configured maximum)
- **Snooze**: Short-term deferral (configurable, default 4 hours)
- **Install at Login**: Schedule installation for next user login

---

## Diagnostics

For troubleshooting, the script can generate a comprehensive diagnostic report that includes:
- System configuration details
- Dependency status
- Deferral state
- Environment variables
- LaunchDaemon status
- Recent log entries

This report is saved to `/Library/Logs/erase-install-diagnostics.txt`.

---

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

---

## Author

> Made with ❤️ by [MacJediWizard Consulting, Inc.](https://macjediwizard.com)
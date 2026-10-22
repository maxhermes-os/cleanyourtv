# Philips Google TV TA5 (Germany / Europe)

Philips Google TV TA5 (TPV / TP Vision, board `PH1M_WW_9972`, MediaTek `mt5896` "merak"), Google TV 14 (API 34), build `UKN2.241117.001`, ~2.85 GB RAM.
Debloated and configured with the Clean Your TV launcher on 2026-10-22.

| File | What it is |
|---|---|
| `debloat.txt` | Disabled telemetry, ACR tracking, promo apps, and unused bridges (`setupwraith` included after Wi-Fi re-join) |
| `../../launcher/app/src/main/res/values/config.xml` | 6-column dock (YouTube, Netflix, Disney+, Apple TV, MagentaTV, waipu.tv), Live TV (`org.droidtv.playtv`), Philips remote key mapping (`141` gear, `813` Apps) |

## Quick Commands (Windows PowerShell)

All commands run from `F:\Projekte\cleanyourtv`:

```powershell
# 1. Check if a firmware update re-enabled any bloatware (and fix it automatically)
tools\venv\Scripts\python.exe -I tools\check.py examples\philips-google-tv-ta5\debloat.txt --fix

# 2. Re-apply the debloat list manually
powershell -ExecutionPolicy Bypass -File tools\disable.ps1 -TvHost 192.168.68.115 examples\philips-google-tv-ta5\debloat.txt

# 3. Rebuild and reinstall the customized launcher (with HomeKeyService for remote buttons)
powershell -ExecutionPolicy Bypass -File launcher\build-and-install.ps1 -TvHost 192.168.68.115 -HomeKeyService

# 4. Undo everything (re-enables all disabled packages and restores the stock Google TV launcher)
powershell -ExecutionPolicy Bypass -File tools\restore.ps1 -TvHost 192.168.68.115 examples\philips-google-tv-ta5\debloat.txt com.google.android.apps.tv.launcherx
```

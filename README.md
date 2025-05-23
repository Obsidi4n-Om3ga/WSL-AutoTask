# WSL-AutoTask
Automatically runs a PowerShell script after Windows Update reboot using Event ID 19 trigger.

# 🧠 Auto-Run WSL Check After Windows Update

Automatically run a PowerShell script after a successful **Windows Update reboot** using **Task Scheduler** and Windows Event Log monitoring.

## 🎯 Goal

Run your `Check-WSL-PostUpdate-AutoReboot.ps1` script immediately after Windows completes installing an update and reboots — without requiring any user input.

---

## ⚙️ Trigger Mechanism

We utilize **Windows Event ID 19** from the `System` log, which signifies a successful Windows Update installation followed by a reboot.

### 🎯 Tracked Event
| Field   | Value |
|---------|-------|
| Log     | System |
| Source  | Microsoft-Windows-WindowsUpdateClient |
| Event ID | 19 |
| Meaning | "Installation Successful" (post-update reboot) |

---

## 🛠️ Step-by-Step Setup

### 🔧 1. Place Your Script
Ensure your `.ps1` script is saved at a stable path, e.g.:

```plaintext
C:\Scripts\Check-WSL-PostUpdate-AutoReboot.ps1

📅 2. Open Task Scheduler

    Press Win + S and search for Task Scheduler

    Click Create Task… (not Basic Task)

🧩 3. General Tab

    Name: Run WSL Check After Windows Update

    Run with highest privileges: ✅

    Configure for: Windows 11

📌 4. Triggers Tab

    Begin the task: On an event

    Set the following:

        Log: System

        Source: Microsoft-Windows-WindowsUpdateClient

        Event ID: 19

💻 5. Actions Tab

    Action: Start a program

    Program/script: powershell.exe

    Add arguments:

    -ExecutionPolicy Bypass -File "C:\Scripts\Check-WSL-PostUpdate-AutoReboot.ps1"

🧼 6. Conditions and Settings Tab

    Uncheck: “Start the task only if the computer is on AC power” (optional)

    Check:

        “Allow task to be run on demand”

        “If the task fails, restart every: 1 minute, up to 3 times”

✅ Result

Now, every time Windows completes an update and reboots, your WSL check script will:

    Run automatically

    Verify or update the WSL kernel

    Prompt for reboot if needed
MIT License

Copyright (c) 2025 Obsidi4n-Om3ga

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


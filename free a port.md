To kill a process running on port **3001** in Windows, follow these two steps using the Command Prompt (CMD) or PowerShell.

### Alternative: Use PowerShell (One-Liner)

If you are using **PowerShell**, you can do this in a single command without looking up the PID manually:

```powershell
Stop-Process -Id (Get-NetTCPConnection -LocalPort 3001).OwningProcess -Force
Stop-Process -Id (Get-NetTCPConnection -LocalPort 5173).OwningProcess -Force
```

### 1. Find the Process ID (PID)

Open your terminal (CMD or PowerShell) and run the following command to identify which process is using the port:

```cmd
netstat -ano | findstr :3001

```

Look at the **last column** of the output. That number is the **PID** (Process ID).

* **Example Output:** `TCP 0.0.0.0:3001 0.0.0.0:0 LISTENING 12345`
* In this case, the PID is `12345`.

---

### 2. Kill the Process

Once you have the PID, run the `taskkill` command to stop it. Replace `12345` with the number you found in Step 1:

```cmd
taskkill /PID 12345 /F

```

* `/PID` specifies the Process ID.
* `/F` forces the process to terminate.

---

### Alternative: Use PowerShell (One-Liner)

If you are using **PowerShell**, you can do this in a single command without looking up the PID manually:

```powershell
Stop-Process -Id (Get-NetTCPConnection -LocalPort 3001).OwningProcess -Force
Stop-Process -Id (Get-NetTCPConnection -LocalPort 5173).OwningProcess -Force
```

### Quick Troubleshooting

* **Access Denied:** If you get an "Access Denied" error, right-click your Command Prompt or PowerShell icon and select **"Run as Administrator"**.
* **Port still busy:** Sometimes multiple processes (or child processes) might be using the port. Re-run the first command to see if a new PID has appeared.

Would you like me to show you how to automate this with a script so you don't have to type it every time?

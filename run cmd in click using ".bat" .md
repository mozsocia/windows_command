### 🔴 
give me windows powershell or cmd script which will do 
- open a cmd in current directory and run "npm run dev"
- and open a cmd in currentdirectory/viteapp and run "npm run dev"
---

Here are two scripts to achieve your goal: one for PowerShell and one for CMD. Both will open two separate command prompt windows, one in the current directory to run `npm run dev`, and another in the `viteapp` subdirectory to run `npm run dev`.

### PowerShell Script
Save this as `run_dev.ps1`:

```powershell
# Get the current directory
$currentDir = Get-Location

# Open a new CMD window in the current directory and run npm run dev
Start-Process cmd -ArgumentList "/k cd /d `"$currentDir`" && npm run dev"

# Open a new CMD window in the viteapp subdirectory and run npm run dev
$viteAppDir = Join-Path $currentDir "viteapp"
Start-Process cmd -ArgumentList "/k cd /d `"$viteAppDir`" && npm run dev"
```

**How to run:**
1. Save the script as `run_dev.ps1` in your project directory.
2. Open PowerShell in the project directory.
3. Run the script with:
   ```powershell
   .\run_dev.ps1
   ```

This will open two CMD windows, each running the respective `npm run dev` command.

### CMD Script
Save this as `run_dev.bat`:

```batch
@echo off
:: Open a new CMD window in the current directory and run npm run dev
start cmd /k "cd /d %CD% && npm run dev"

:: Open a new CMD window in the viteapp subdirectory and run npm run dev
start cmd /k "cd /d %CD%\viteapp && npm run dev"
```

**How to run:**
1. Save the script as `run_dev.bat` in your project directory.
2. Double-click the `.bat` file, or run it from CMD with:
   ```cmd
   run_dev.bat
   ```

This will open two CMD windows, one in the current directory and one in the `viteapp` subdirectory, each running `npm run dev`.

### Notes
- Ensure the `viteapp` directory exists in the current directory, or the second command will fail.
- The `/k` flag keeps the CMD windows open after running the command, so you can see the output. If you want the windows to close after execution, replace `/k` with `/c`.
- Make sure `npm` is installed and the `dev` script is defined in the `package.json` files in both directories.
- The PowerShell script requires execution permissions. If you encounter a permission error, run:
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
   ```

Choose the script that best fits your environment (PowerShell or CMD).

---
#### 🔴 i have "terminal" app installed from windows app store , can you please use it to run those command in "terminal" app two tab?

To run the two commands (`npm run dev` in the current directory and `npm run dev` in the `viteapp` subdirectory) in two separate tabs of the Windows Terminal app, you can use the `wt` (Windows Terminal) command to automate this. Below is a CMD batch script that opens Windows Terminal with two tabs, each navigating to the respective directory and running `npm run dev`.

### CMD Script for Windows Terminal
Save this as `run_dev.bat`:

```batch
@echo off
:: Get the current directory
set "currentDir=%CD%"

:: Open Windows Terminal with two tabs
wt -p "Command Prompt" -d "%currentDir%" cmd /k npm run dev ; new-tab -p "Command Prompt" -d "%currentDir%\viteapp" cmd /k npm run dev
```

**How to run:**
1. Save the script as `run_dev.bat` in your project directory.
2. Double-click the `.bat` file, or run it from CMD with:
   ```cmd
   run_dev.bat
   ```
3. This will launch Windows Terminal with two tabs:
   - The first tab opens in the current directory and runs `npm run dev`.
   - The second tab opens in the `viteapp` subdirectory and runs `npm run dev`.

### Explanation
- `wt`: The Windows Terminal command-line interface.
- `-p "Command Prompt"`: Specifies the profile to use (Command Prompt). You can replace it with another profile (e.g., "Windows PowerShell") if preferred.
- `-d "%currentDir%"`: Sets the working directory for the first tab to the current directory.
- `-d "%currentDir%\viteapp"`: Sets the working directory for the second tab to the `viteapp` subdirectory.
- `cmd /k npm run dev`: Runs `npm run dev` in a CMD shell and keeps the tab open to display output.
- `; new-tab`: Opens a new tab in Windows Terminal for the next command.

### Notes
- **Windows Terminal**: Ensure the Windows Terminal app is installed from the Microsoft Store and accessible via the `wt` command. If `wt` is not recognized, verify that Windows Terminal is added to your system’s PATH or use the full path to `wt.exe` (e.g., `C:\Users\<YourUsername>\AppData\Local\Microsoft\WindowsApps\wt.exe`).
- **Directory Check**: The `viteapp` directory must exist in the current directory, or the second tab will open but fail to run the command.
- **Profile Name**: If you’ve customized your Windows Terminal profiles, ensure `"Command Prompt"` matches an existing profile name in your Terminal settings (`settings.json`). You can check this by opening Windows Terminal, clicking the dropdown arrow, and selecting "Settings" > "Profiles".
- **Keeping Tabs Open**: The `/k` flag ensures the tabs remain open to show the `npm run dev` output. Replace `/k` with `/c` if you want the tabs to close after the command finishes.
- **NPM Requirements**: Ensure `npm` is installed, and the `dev` script is defined in the `package.json` files in both the current directory and the `viteapp` subdirectory.

### Alternative: PowerShell Script
If you prefer PowerShell, here’s an equivalent script (`run_dev.ps1`):

```powershell
# Get the current directory
$currentDir = Get-Location

# Open Windows Terminal with two tabs
wt -p "Command Prompt" -d "$currentDir" cmd /k npm run dev `; new-tab -p "Command Prompt" -d "$currentDir\viteapp" cmd /k npm run dev
```

**How to run:**
1. Save as `run_dev.ps1`.
2. Open PowerShell in the project directory and run:
   ```powershell
   .\run_dev.ps1
   ```
3. If you encounter a permission error, set the execution policy:
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
   ```

This achieves the same result as the CMD script but uses PowerShell syntax.

### Source Reference
The approach is based on Windows Terminal’s command-line capabilities, as described in articles like "Run Multiple Services by One Click [Windows Terminal]" by Giri Aakula, which demonstrates opening multiple tabs with specific commands.[](https://giriaakula.medium.com/run-multiple-services-by-one-click-windows-terminal-2d5748a89286)

Let me know if you need further clarification or customization!


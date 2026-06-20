# PowerShell Guide — Class Schedule Report (Advanced)

This is the original, command‑line approach. It produces the same report as the web app but runs from **PowerShell on Windows** (with Microsoft Excel installed). Handy for automation or if you prefer scripting.

> **Prefer the easy way?** Most people should use the **[Web App Guide](WEB-APP-GUIDE.md)** — no install, no admin, no Excel, and it reads `.xls` directly.

> **Note:** You only do the setup/configuration **once**. After that, just re‑run the command in [Step 9](#step-9--generate-the-report) any time you need a fresh report.

> 📷 _Screenshot placeholder — overview of the finished report. (Add an image here, e.g. `images/ps-0-overview.png`.)_

---

## What you'll need

- A **Windows** PC with **Microsoft Excel** installed (Excel is used to read the spreadsheet).
- The **`Generate-ClassReport.txt`** file from this repo.
- Your class data export from **BlackPug** → <https://scoutingevent.com/>

---

## One‑time setup

### Step 1 — Save the script
Save the **`Generate-ClassReport.txt`** file to your **Downloads** folder.

> 📷 _Screenshot placeholder — the file saved in Downloads._

### Step 2 — Rename the extension
Change the file extension from **`.TXT`** to **`.PS1`**, so it becomes:

```
Generate-ClassReport.ps1
```

> If you don't see file extensions, open **File Explorer → View → Show → File name extensions** and turn it on.

> 📷 _Screenshot placeholder — renaming .txt to .ps1._

### Step 3 — Get your data from BlackPug
Log in to **<https://scoutingevent.com/>** and download your class data **`.XLS`** export.

### Step 4 — Convert to `.XLSX`
Open the `.XLS` file in Excel, then **File → Save As → Excel Workbook (`.xlsx`)** and save it to your **Downloads** folder.

> **Why?** Recent versions of Office block the legacy `.xls` format from automated reading. Saving as `.xlsx` avoids that. *(The web app does not require this step.)*

> 📷 _Screenshot placeholder — Save As → Excel Workbook (.xlsx)._

### Step 5 — Open PowerShell as Administrator
Go to the **Start Menu**, type **"PowerShell"**, then **right‑click → Run as administrator**.

> 📷 _Screenshot placeholder — Run as administrator._

### Step 6 — Allow scripts to run
Type the following and press **Enter**, then press **`Y`** (yes) when prompted:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
```

> **Tip:** `RemoteSigned` is safer than `Unrestricted` and still lets your local script run.

> 📷 _Screenshot placeholder — Set-ExecutionPolicy prompt._

### Step 7 — Go to the root of your C: drive
```powershell
cd \
```

### Step 8 — Navigate to your Downloads folder
Use **Tab** to auto‑complete folder names:

```powershell
cd .\Users\
```
Press **Tab** until you reach your user account, then type **`\d`** and press **Tab** to complete **Downloads**. You should end up with something like:

```powershell
cd .\Users\kenHausman\Downloads\
```

> 📷 _Screenshot placeholder — navigating to the Downloads folder._

---

## Step 9 — Generate the report

Run the script, pointing it at your `.xlsx` file:

```powershell
.\Generate-ClassReport.ps1 -InputPath "C:\Users\kenHausman\Downloads\962G_Class_Data_-_Excel_2026_06_19.xlsx"
```

The script creates an **HTML report** and opens it automatically in your browser.

> 📷 _Screenshot placeholder — running the command in PowerShell._

---

## Running a multi‑troop ingest

Merge **multiple troop exports** into a single report, then use the **Unit** filter to separate them:

```powershell
# Several files explicitly
.\Generate-ClassReport.ps1 -InputPath "Troop962G.xlsx","Troop17B.xlsx","Pack5.xlsx"

# Or merge everything matching a wildcard
.\Generate-ClassReport.ps1 -InputPath "C:\Users\kenHausman\Downloads\*.xlsx"
```

Read the comment block at the top of `Generate-ClassReport.ps1` for full details and more examples.

---

## Refreshing later

After the one‑time setup, you **don't** need to repeat Steps 1–7. Just open PowerShell, `cd` to your Downloads folder, and re‑run the command from **Step 9** whenever you need an updated report.

---

*Prefer a one‑click, no‑install option? See the [Web App Guide](WEB-APP-GUIDE.md).*

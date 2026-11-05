# Revit Batch Studio

**Unattended, crash-proof batch processing for Revit 2021–2027.**
Export NWC, IFC, DWG, DGN, DWF, PDF and images, or run Dynamo and Python on dozens of models — overnight, hidden in
the background, while you do something else.

[**⬇ Download the latest version**](https://github.com/OsmanMohamed21/RevitBatchStudio/releases/latest) · one file, about 2 MB

---

## Why
Batch exports in Revit stop for the wrong reasons: a dialog nobody answers, a model that crashes Revit, a hang in the
NWC or IFC exporter, a file that is still open. Revit Batch Studio runs every model in a supervised Revit session,
answers dialogs, detects hangs and crashes, retries what can be retried and continues exactly where it stopped.

## Features
- **Exports:** NWC (same options as *Navisworks Options Editor – Revit*), IFC (all exporter options), DWG, DGN,
  DWF/DWFx, PDF (Revit's own exporter) and images — with **Choose sheets** to pick exactly which sheets.
- **Your own automation:** Dynamo graphs (.dyn), Python scripts (.py) and compiled .dll code on every model.
- **Robust:** watchdog for hangs, automatic dialog answers, crash recovery, retries, quarantine of broken models,
  outputs verified before they are delivered — a finished export is never lost.
- **ACC / Autodesk Docs (Forma):** cloud models and Desktop Connector folders.
- **Schedules:** daily or weekly runs with Windows Task Scheduler, plus **Teams / e-mail notifications**.
- **Fast:** Revit works hidden in the background and stays open between runs.
- **Settings as XML:** import and export the options of every task.
- English and Arabic interface, light and dark themes. Signed automatic updates.

## Requirements
- Windows 10 or 11 (64-bit) and Autodesk Revit 2021–2027.
- [.NET 10 Desktop Runtime (x64)](https://dotnet.microsoft.com/download/dotnet/10.0) — if it is missing, Windows
  offers Microsoft's download when you start the app.
- For NWC export: the *Navisworks NWC Export Utility* for your Revit version.

## Quick start
1. Download `RevitBatchStudio-<version>.exe` (or the `.zip` if your browser blocks .exe files) from
   [Releases](https://github.com/OsmanMohamed21/RevitBatchStudio/releases/latest).
2. Put it in a folder of your own (for example *Documents\RevitBatchStudio*) and double-click it. No installation,
   no administrator rights, no command line.
3. Read and accept the license and privacy notice.
4. **Job** tab: add models, add tasks, click **Run job**. The **Runs** tab shows the progress live.

## Privacy
The app sends usage and diagnostic data to the developer, as explained in the notice you accept at the first start
and in [PRIVACY.md](PRIVACY.md).

## Support
Questions, bugs and ideas: [open an issue](https://github.com/OsmanMohamed21/RevitBatchStudio/issues/new/choose).
Please attach `%LOCALAPPDATA%\RevitBatchStudio\Logs\startup.log` or the run's log from the **Runs** tab when
something fails.

## Author
Designed and developed by **Eng. Othman Muhammad** — [linkedin.com/in/osmanz](https://www.linkedin.com/in/osmanz/) ·
[bimminutes.com](https://bimminutes.com)

---

<div dir="rtl">

## بالعربي
**Revit Batch Studio** أداة لتصدير وتشغيل المهام على عدد كبير من نماذج Revit (من 2021 إلى 2027) بشكل آلي ومحصّن
ضد الأعطال: NWC وIFC وDWG وDGN وDWF وPDF والصور وDynamo وPython، مع جدولة وإشعارات Teams/البريد ودعم نماذج ACC.
ملف واحد حجمه حوالي 2 ميجا بدون تثبيت — [حمّل أحدث إصدار](https://github.com/OsmanMohamed21/RevitBatchStudio/releases/latest).

</div>

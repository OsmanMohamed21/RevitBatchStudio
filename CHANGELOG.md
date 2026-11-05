# Changelog

## 1.9.5 — update message at start, sheet picker reads models itself

- **Update message at every start:** "A new version is ready" with *Update now* / *Skip (N left)*. Each skip counts;
  after two, the app explains that the update is now needed and can only be updated or closed. Not asked again when
  closing after a skip.
- **Choose sheets opens the models itself:** models Batch Studio has not opened yet are read right away in a hidden
  Revit; each model shows "Opening the model in Revit…" and fills in with its real sheets as soon as it is read (or
  says why it could not be read).
- Fixed: the sheet-reading run could not be created (its name contained an en dash).
- A Revit kept open by an older version of the app never takes a run from a newer one (its add-in would be older).

## 1.9.4 — choose sheets, usage steps, clearer update errors, faster commits

- **Choose sheets…** on PDF, DWG, DGN, DWF and image tasks: a searchable list of each model's sheets (natural order:
  A-2 before A-10), select all / none, per model. Lists are saved every time Batch Studio opens a model; models not
  read yet are read by a small background run (*Read sheets*), which also leaves Revit open for the export. Chosen
  sheets are stored as `model::sheet number` (export / import with the task's XML).
- **Usage steps** (funnel): privacy accepted, models added, sheets picked, schedule created (once per installation),
  run started and update postponed (every time). Code.gs: new `step` column and funnel rows in the summary.
- **Clear update errors:** an invalid signature now says the sheet row is not the signed row and how to paste it
  again; Code.gs tolerates spaces / case changes in the sha256 and signature cells; a download that is not a Windows
  program (e.g. a zip) is never installed.
- **Faster exports with many files:** one shared stability wait for all files of a task (a 30-sheet DWG export used to
  wait 30 times).

## 1.9.3 — the App Store copy updates itself too

- The Autodesk App Store package now contains the same program, updating itself from the same signed releases; it
  also brings the package's Revit add-in to the same version.
- An update is only *required* (after two postponements) when the program can replace itself; where it cannot (a
  per-machine install), it is offered only, so nobody is locked out.

## 1.9.2 — updates can be postponed twice

- A new version can be postponed **twice** (*Later* at start or *Not now* when closing, counted once per session; the
  banner says how many are left). At the next start the update is required: the app can only be updated or closed.
  If the update server cannot be reached then, the app asks to connect and retry. Scheduled (unattended) runs are
  never blocked. *Skip this version* was removed.

## 1.9.1 — checked against the Revit API, faster start, App Store package

- **Every export option name was checked against Revit's own API files (2021, 2024, 2025, 2027).** Two PDF fixes
  came out of it: Revit's PDF options have no margin type, so *Offset from corner* now maps to LowerLeft / Margins;
  *Remove lines using* maps to Revit's raster setting (it was ignored). PDF now also has **Paper Format** and
  **Orientation** (*Appearance & Layout*); *Keep Paper Size & Orientation* is off by default.
- **Faster start:** past runs, the usage-data check and the Revit detection load in the background, so the window
  opens at once even with hundreds of runs; finished runs are no longer re-read at every start.
- **Autodesk App Store package** (`…-AutodeskAppStore.zip`, see docs/AUTODESK-APP-STORE.md): store edition without
  self-update; the app uses the store's add-in instead of installing a second copy.

## 1.9.0 — sheet export settings, DGN, DWF, images

- **PDF, DWG and IFC settings rebuilt option by option**, in groups: Paper Placement, Zoom, Printer, Hidden Line Views,
  Appearance, Options and File (PDF); export setup, external references and .pcp clean-up (DWG); General, Additional
  Contents, Level of details, Property Sets and Advanced (IFC, with the IFC exporter's own options).
- **New tasks:** Export DGN (model export setups), Export DWF / DWFx (with paper placement, zoom, hidden lines,
  appearance and options), Export images (fit to pixels or zoom, PNG/JPG/TIFF..., optional HTML page of all images).
- Each task's settings import / export as XML (Import XML... / Export XML...).

## 1.8.0 — Revit kept open, checks before Revit starts, notifications

- **Revit kept open between runs** (*Execution ▸ Keep Revit open after a run*, default 10 min, 0 = off): the runner
  keeps the hidden Revit after a run and the next run (from the app or a schedule) starts at once instead of waiting
  1-2 minutes. Only jobs that would start Revit the same way share it; Revit closes when the time is up.
- **Checks before work starts:** output folders are tested before any Revit starts (a model whose exports could not be
  saved fails in seconds); a model whose task cannot run on this PC (no NWC exporter, no Dynamo) fails before it is
  opened.
- **Notifications after scheduled runs:** a Teams channel workflow or a Power Automate flow (which can send an e-mail)
  receives the result as a card: outcome, summary, failed models. *Schedules* page: webhook URL, "only when a model
  failed", *Send test*.

## 1.7.1 — fixes from the usage data

- **Cloud models open again:** Revit's API refuses to detach cloud models ("Detach option is not valid for cloud
  model"), so every cloud run failed. They now open from Revit's local cache (only changes are downloaded); nothing is
  synchronized to the cloud, and anything a task borrowed is relinquished before closing.
- **A finished export is never lost because the old file is open:** if the existing NWC/PDF/... is open in Navisworks
  or read-only, the new one is saved next to it as "name (2).nwc" with a warning, instead of failing and redoing the
  whole model.
- **Revit really stays hidden:** its main window is found by itself (the API handle was not available at start-up) and
  hidden again after every open.
- Usage data: failure kinds now say what failed (CorruptModelException, AccessDenied, Crashed...); a run is never
  reported twice when two Batch Studio windows are open (e.g. a scheduled start). Summary: average duration rounded.

## 1.7.0 — Dynamo & Python, Revit in the background, faster

- **Run Dynamo graph (.dyn)** and **Run Python script (.py)** tasks, using the Dynamo installed with each Revit version
  (nothing extra ships). Python gets `doc`, `uidoc`, `uiapp`, `app`, `ARGS`, `OUTPUT_FOLDER`; `print()` goes to the
  runner log and a Python error fails the task with its traceback. Engine: Auto, CPython3, PythonNet3 or IronPython2.
- **Revit works hidden** in the background; the runner log shows the progress as before. *Execution ▸ Show Revit while
  it works* shows it for troubleshooting.
- **Worksets ▸ Editable**: opens the worksets owned by the Revit user, like Revit's Open dialog.
- **Faster and lighter:** the update check runs after the
  window is on screen; closing reuses the start-up answer (no network wait); the Revit add-ins are no longer re-read at
  every start. File settings (scripts, assemblies) get a *Browse…* button.

## 1.6.1 — the one-file exe opens on locked-down PCs

- **Fix: the one-file exe did not open** (double-click did nothing). 1.5.0 and 1.6.0 carried their own .NET (64 MB) and
  unpacked WPF's DLLs into `%TEMP%` at every start, which locked-down PCs (AppLocker, EPM, antivirus) block silently.
  The exe now uses the installed .NET 10 Desktop Runtime like the folder edition: **about 2 MB**, nothing unpacked to
  `%TEMP%`. (A build flag was also silently ignored; the build now fails if any DLL would sit next to the exe.)
- **A failed start is never silent:** Windows' message box says what went wrong, the details are saved in
  `%LOCALAPPDATA%\RevitBatchStudio\Logs\startup-error.log`, and `startup.log` lists the steps of the last start. A
  failure while the window is being created no longer leaves an invisible process behind.
- **The owner's telemetry.json is built in**, byte for byte (`build/telemetry.json`), for usage data and updates.
- **Updates are checked only when the app starts (banner) and when it is closed** (one question: *Update and close ·
  Not now · Skip this version*); no more timer. *Later* hides the banner until closing.
- Google Drive (and Dropbox) share links work as download links.

## 1.6.0 — automatic update check

- **Updates**: the app checks for a new version at start-up and every 6 hours and shows a banner (What's new, Skip this
  version, Later, Update now). *Update now* downloads the new exe, verifies the owner's signature and the SHA-256, swaps
  the program and restarts. *About ▸ Check for updates*. See docs/UPDATES.md.
- Releases are published from the Google Sheet (**releases** tab, served by the same Apps Script) or a static
  latest.json. **tools/release-signer/ReleaseSigner.html** signs a release in the browser (offline, no commands) and
  copies the row to paste; `build/sign-release.sh` does the same in the build.
- The usage-data address and the update address are compiled in (build/release.json): the one-file exe needs no
  telemetry.json next to it.

## 1.5.0 — one-file edition

- **`RevitBatchStudio-<version>.exe`**: the whole product in one self-contained file (no .NET installation needed):
  desktop app, batch runner (`--cli`, what `rbs.exe` is in the folder edition) and the Revit add-ins for 2021–2027.
  Any file name and location work; Revit's *Batch Studio* button starts that exact file.
- The desktop app starts its runner as a hidden copy of itself in the one-file edition, so closing the window still
  never stops a batch.
- *Copy SHA-256 for IT* hashes only the program file in the one-file edition.
- File properties now show the publisher (Eng. Othman Muhammad, bimminutes.com).
- The folder edition (zip) is unchanged and remains the choice for IT-managed PCs.

## 1.4.1

- Fixed: saving the first schedule failed with "The system cannot find the file specified (0x80070002)" and fell back
  to "runs only while the app is open". The *Revit Batch Studio* folder of Task Scheduler did not exist yet, and the
  "not found" answer of Windows was not recognised as such, so the folder was never created. Schedules saved with 1.4.0
  just need *Save* again.
- A Task Scheduler failure now names the step (connect / folder / register) and the Windows error code.

## 1.4.0 — schedules and ACC models

- **Schedules** (new page, and *Schedule…* on the Job page): run a job on chosen days at a time into a chosen folder,
  optionally in a dated sub-folder per run and waking the PC. Registered in Windows Task Scheduler through its API (no
  command line, no admin rights); the app starts minimized, runs the batch and closes. Missed times run when the PC is
  back on. If Windows refuses the task, the schedule runs while the app is open. *Run now* runs it immediately.
- **ACC / BIM 360 models made easy:** new Revit button *Add-Ins ▸ Revit Batch Studio ▸ Add cloud model* captures the
  open cloud model; *Job ▸ Models ▸ Add cloud models…* adds the captured models. The model name is kept, so outputs and
  reports use it instead of a GUID.
- Outputs are copied under a `~$….tmp` name before the final rename, so sync clients (Autodesk Desktop Connector,
  OneDrive) never upload a half-written file — choose a Desktop Connector folder to get the exports into ACC Docs.
- Fixed: the Revit *Batch Studio* button mentioned the removed `Install.cmd`.

## 1.3.3

- Fixed: the per-model list overwrote the model count in the report (`models` showed `[object Object]`, the summary
  counted 0 models processed). The list is now `modelList`; `Code.gs` writes it to the `models` tab.
- Fixed (`Code.gs`): number-like text such as `2022,2026,2027` or `1.3.2` was turned into a number/date by Sheets.
- About: the *Privacy and license* section (status, last report, test connection) was removed; sends are still logged
  in `%LOCALAPPDATA%\RevitBatchStudio\telemetry.log`.

## 1.3.2

- **About ▸ Test connection**: sends a test row to the Google Sheet and explains which step fails (missing or
  misnamed `telemetry.json`, invalid JSON, `/dev` URL, Google sign-in page because the deployment is not open to
  *Anyone*, outdated script, script not authorised, network/proxy/security product). Every send is logged in
  `%LOCALAPPDATA%\RevitBatchStudio\telemetry.log`, and About shows the result of the last send.
- Company proxies that need the Windows sign-in (NTLM/Kerberos) now work.
- `telemetry.json` may contain comments or a trailing comma; a misnamed `telemetry.json.txt` is detected.
- `Code.gs` accepts the `test` event (paste the new version and deploy a new version).

## 1.3.1

- **License and privacy notice on first start.** MIT License plus the description of the data sent for analysis;
  *I accept* is enabled only after scrolling to the end, *Decline and exit* closes the app. Readable again in
  *About ▸ Privacy and license*. Replaces the opt-in banner and the About checkbox.
- **Analysis data extended** (as stated in the notice): Windows user, computer and domain names, job name, model
  names and paths, task settings and the result of every model (new `models` tab in the Google Sheet), app error
  messages. Updated `tools/telemetry/Code.gs` (columns are appended, existing rows stay aligned).
- The unsigned add-in prompt is answered **Always Load** again (fallback *Load Once*).
- *Revit & add-in*: the add-in path column was removed.
- Setup guide: where the *Web app* type hides in *Deploy ▸ New deployment* (the gear icon next to *Select type*).

## 1.3.0 — professional UI, Arabic, safer defaults

**Navisworks NWC settings**
- The NWC task now mirrors *Navisworks Options Editor – Revit*: the same 19 options with the same captions, order and
  defaults (Export = Entire project, Export room geometry on, Embed Textures, Separate Custom properties, Type
  properties on Elements…), laid out as a compact multi-column property grid with a description on hover.
- Embed Textures, Separate Custom properties, Strict Sectioning and Type properties on Elements have no Revit API
  counterpart: they are marked ⓘ, written to XML, and the run log states that Revit takes them from Navisworks Options
  Editor on the batch PC.
- **Import / export XML** for every task's settings (also reads options exported from Navisworks Options Editor;
  unknown options are reported, never guessed; out-of-range numbers are rejected).

**Desktop app**
- New layout: navigation rail, resizable panes everywhere (splitters), compact inputs, starts maximized.
- **Light / dark theme** and **Arabic** (complete right-to-left UI), switchable live; remembered per user.
- Runs: *Message* and *Outputs* wrap; every output path is a link that shows the file in Explorer; progress bars.
- Themed, selectable message boxes (error text can be copied for support).
- Developer signature in the top bar, the status bar and *About*, linking to linkedin.com/in/osmanz.

**Execution & Dialogs review (safety)**
- Every Execution / Dialogs number has a safe range, enforced in the app (red, not applied) **and** in the engine
  before Revit starts (`rbs validate`, *Run job*): e.g. a 5 s heartbeat timeout used to kill healthy sessions, a 0 %
  CPU threshold made a frozen Revit look busy forever, a 1-minute stall timeout killed slow exports.
- Consistency warnings: parallel sessions vs. installed memory, quarantine threshold above attempts, timeouts longer
  than the model timeout, unknown-dialog delay longer than the stall timeout, safety switches turned off.
- The add-in security prompt is answered **Load Once**, never *Always Load* (which permanently trusted every unsigned
  add-in on the PC on the user's behalf).
- A user dialog-rules file is validated before the run (precise error per rule); an invalid regular expression used to
  break the watchdog's dialog pass on every tick. Patterns now have a 250 ms timeout and one bad rule is skipped,
  never the watchdog.
- **Keep the PC awake** during a batch (new, on by default): Windows sleep used to stop overnight batches.
- *Revit shutdown* timeout and *Revit language* (validated list) are now editable; in-Revit dialog answers are
  validated (`DialogId=code`).

**Anonymous usage statistics (opt-in)** — Google Sheet collector (`tools/telemetry/Code.gs`), consent banner, *About*
page with "show exactly what is sent". Not active in this package until an endpoint is configured
([docs/TELEMETRY.md](docs/TELEMETRY.md)).

## 1.2.0 — works on locked-down PCs

Reported: antivirus / EPM flags every command-line action, so `Install.cmd` and `rbs …` cannot run.
- **No command line needed anywhere.** New *Revit & add-in* tab: installed Revit versions, add-in status,
  **Install / repair**, **Remove**, open the add-ins folder. A banner offers the install on first start; runs still
  install the add-in automatically.
- **Removed `Install.cmd` / `Install.ps1`.** A batch file launching PowerShell with `-ExecutionPolicy Bypass` is a
  pattern security products flag as malware.
- **No more "Mark of the Web" removal.** 1.0.1–1.1.0 deleted the downloaded-file mark of the deployed add-in, a known
  defense-evasion technique that security products detect. The add-in is now written as a fresh local file, the
  way every installer writes its files; Revit 2021–2024 still load it.
- **Runs inside the app when `rbs.exe` is blocked**: if the runner cannot start (or stops immediately), the app
  offers to run the batch in its own window; a setting makes that the default. Closing the window then asks first.
- **For IT**: *Copy SHA-256 list for IT* in the app and `SHA256SUMS.txt` in the package, to allow-list the files.


## 1.1.0

From the "Purge & NWCs" run (8 models in Revit 2022: every NWC exported, every purge failed, Revit killed at the end):

**Fixed**
- **Purge on Revit 2021–2023**: `Document.GetUnusedElements` only exists in Revit 2024+. Older versions now purge
  unused families and types through the Performance Adviser rule ("Project contains unused families and types").
- **Revit not closing after the batch**: dialogs were no longer answered once a session started to stop, so a
  dialog shown on exit could only end with a kill after 90 s. Dialogs are now answered while closing, the main window
  is asked to close before any kill, and any dialog seen while closing is logged.
- **Run outcome**: a run where models were only partially processed is now `CompletedWithFailures` (exit code 1),
  not `Completed`.

**New**
- Planner warnings before the run (runner log, GUI before *Run*, `rbs validate`): a Purge without a later SaveAs is
  discarded when the model closes (and does not change NWC/IFC/DWG/PDF exports); PDF export needs Revit 2022+.
- **Brand identity**: app icon, CLI icon, Revit ribbon icons, logo and banner (`assets/branding`, generated by
  `build/branding/generate.py`).
- **Revit ribbon button**: in interactive Revit sessions the add-in adds *Add-Ins → Batch Studio*, which opens the
  desktop application (no event handlers, nothing in the background; batch sessions are unchanged).
- **`Install.cmd`** in the package: unblock files, check the .NET 10 Desktop Runtime, `rbs addin install`,
  Start Menu and Desktop shortcuts.

## 1.0.2

**Fixed — run monitor went blank and could not be brought back** (reported after a successful run: selecting or
double-clicking the run showed nothing). Refreshing the runs list cleared and rebuilt the bound collection; WPF
then dropped the selection, the monitor was discarded, and re-selecting the same run did not rebuild it. The list
is now updated in place (selection kept) and the monitor is rebuilt whenever it is missing.

**Outputs are now one click away**
- **📂 Outputs** button and the outputs path (selectable, copyable) in the run monitor header.
- Double-click a run → opens its outputs folder; double-click a model → Explorer with its exported file selected.
- `rbs status <run> [--outputs]` prints the outputs folder (and lists every exported file).

## 1.0.1

**Fixed — agent could not be loaded by Revit 2021–2024** (reported: 2 models exported in Revit 2026, the third,
routed to Revit 2022, failed after 3 × 15 min with "External Tools – External Tool Failure").
- Revit is no longer pointed at the extracted package. The agent is deployed to
  `%LOCALAPPDATA%\RevitBatchStudio\Agent\<year>\<content-hash>\`, with the "downloaded from the internet" mark
  (Zone.Identifier) removed. .NET Framework (Revit 2021–2024) refuses marked or network-located DLLs;
  .NET 8/10 (Revit 2025+) ignores the mark, which is why only Revit 2022 failed. Content-addressed folders also
  make updates safe while a Revit still has the old DLL loaded. Existing manifests self-heal on the next run.
- Startup now **fails fast**: when Revit shows an "External Tools …" dialog and the agent does not connect within
  2 minutes, the session is stopped instead of waiting for the 15 minute startup timeout. The diagnosis quotes the
  add-in load exception from the Revit journal; when it names the agent, no further restarts are attempted.
- `rbs status/resume/pause/continue/cancel` validate the run folder: a quoted path ending with `\"`, the Runs
  folder itself, or a wrong folder now give a clear message instead of an empty status. `latest` = most recent run.
- New: `rbs resume <run> --retry-failed` and a **Retry failed** button: re-run only failed / quarantined models.
- `rbs addin status` / `rbs revit` show where the agent is deployed and whether the package files are blocked.
- 13 new tests (journal parsing, deployment, path resolution, add-in load failure chaos scenarios, retry-failed).

## 1.0.0
Initial release.

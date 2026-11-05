# Privacy

Revit Batch Studio shows this information in a notice that must be read and accepted at the first start.

## What is sent
While you use the app, the following is sent over HTTPS to a Google Sheet owned by the developer (through a Google
Apps Script web app):

1. Your Windows user name, the computer name, the Windows domain and the company network domain (if any), and the
   Windows version.
2. The app version, the interface language and theme, and the Revit versions installed on the computer.
3. For every batch: the job name, the names and full paths of the models, their Revit versions, the tasks (type, name
   and settings), the output folder, the result of every model (status, attempts, duration, messages) and the totals.
4. Usage steps, such as accepting the notice, adding models, choosing sheets, starting a run or postponing an update.
5. Unexpected errors of the app: type, location in the code and message.
6. A random installation number that groups the reports of one installation.

**Not collected:** the content of your models or exported files, passwords, licenses or Autodesk account details.

## Use, access and retention
- **Purpose:** to analyse how the app is used, to diagnose failures and to improve the app.
- **Access:** the developer only (Eng. Othman Muhammad). The data is not sold or shared with third parties. The sheet
  is stored by Google, whose terms apply.

## Your choices
To stop sending data, stop using the app. To ask for a copy of your data or for its deletion, contact the developer
on [LinkedIn](https://www.linkedin.com/in/osmanz/) or through an
[issue](https://github.com/OsmanMohamed21/RevitBatchStudio/issues).

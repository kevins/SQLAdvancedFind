# SQL Advanced Find Bookmarklet for Dynamics 365 / Power Apps

A browser bookmarklet for querying, exploring, and editing Microsoft Dataverse / Dynamics 365 / Power Apps data using SQL directly from your active browser session.

It translates standard SQL queries into FetchXML under the hood and presents the results in an interactive, editable Excel-style grid. This makes it especially useful on locked-down or managed corporate machines where installing external utilities (like XrmToolBox, SQL 4 CDS, or browser extensions) is not permitted.

<img width="1367" height="860" alt="image" src="https://github.com/user-attachments/assets/f04cf2ba-30b9-44c8-98c0-ae1c7ce5af4a" />

---

> [!CAUTION]
> ### ⚠️ Experimental Software & Production Warning
> **There are likely many bugs and edge cases in this codebase.**
> 
> Because this tool translates SQL queries into FetchXML on the fly and supports direct DML operations (row updates, insertions, and deletions) via the Dataverse Web API, **exercise extreme caution if using this in production environments**.
> - Always test your queries and operations in a sandbox or development environment first.
> - Double-check the **Review SQL / Pending Changes** dialog before committing any updates or deletes.
> - Use at your own risk. The author assumes no responsibility for unintended data modifications or data loss.

---

## Why a Bookmarklet?

Most SQL tools for Dataverse require desktop installations (such as XrmToolBox with SQL 4 CDS) or browser extensions. 

This bookmarklet:
- **Zero Installation**: Runs entirely inside your browser's existing session.
- **Inherits Existing Authentication**: Reuses the active session and security role permissions of the logged-in Dataverse user without prompting for credentials.
- **Cross-Platform**: Works anywhere you can use a modern browser (Edge, Chrome, Firefox, Safari).
- **Self-Contained**: Packaged using native browser compression (`DecompressionStream`) so the full application bundle fits in a single bookmark URL.

---

## Installation

1. Create a new browser bookmark / favorite in your browser.
2. Name it something like `SQL Advanced Find`.
3. Open the bookmark settings/editor.
4. Copy the raw bookmarklet code from [`bookmarklet.js`](./bookmarklet.js).
5. Paste the code into the **URL** (or **Location**) field of the bookmark.
6. Ensure the URL starts with `javascript:`.
7. Navigate to any Dynamics 365 or Power Apps model-driven application tab.
8. Click the bookmark to launch the tool.

---

## Features

### 1. SQL Query Editor
- **IntelliSense & Autocomplete**: Autocompletes entity logical names, display names, and attribute names as you type.
- **Multiple Query Tabs**: Work with multiple queries concurrently in separate tabs.
- **File Support**: Open local `.sql` files directly into the editor or save queries to `.sql` files.
- **Keyboard Shortcuts**: Press `Ctrl + Enter` (or `Cmd + Enter`) to run the query immediately.

### 2. SQL to FetchXML Translation
- Automatically converts `SELECT` queries into Dataverse-compatible FetchXML.
- Supports `WHERE` filtering, `ORDER BY`, `JOIN` / `LINK-ENTITY` relationships, `GROUP BY`, and aggregate functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`).
- **FetchXML Preview Tab**: View the exact translated FetchXML generated from your SQL statement before or after execution.

### 3. Interactive Data Grid
- **Workbook-Style Navigation**: Excel-like cell navigation and selection.
- **Multi-Row Selection**:
  - Click row numbers to select rows.
  - Hold `Ctrl` (or `Cmd`) to select/toggle multiple non-contiguous rows.
  - Hold `Shift` to select a continuous range of rows.
  - Click and drag across row numbers to select ranges.
- **Cell Range Selection & Copy**:
  - Drag across cells to highlight a block of data.
  - Right-click to copy with or without column headers.
- **Inline Editing**:
  - Edit cell values directly within the grid.
  - Visual indicators for modified, new, and deleted records.
- **Row Operations**:
  - Add new rows.
  - Duplicate existing rows.
  - Mark rows for deletion.
- **Exporting**:
  - Export query results directly to CSV or Excel.

### 4. Dataverse Integration
- **Personal Views (`userquery`)**:
  - Save SQL queries as Dataverse Personal Views directly into your environment.
  - Overwrite or update existing personal views.
- **DML Review & Confirmation**:
  - Before committing changes (creates, updates, deletes), a review modal displays the exact SQL operations and affected record IDs for confirmation.

---

## How It Works

The bookmarklet source is bundled and compressed with gzip, then encoded in Base64. When clicked, the bookmarklet uses the native browser `DecompressionStream("gzip")` API to inflate the script in-memory and execute it within the context of the active Dataverse page. This allows a complete React-based SQL IDE to launch without hosting external scripts or requiring elevated browser permissions.

---

## Acknowledgements & Credits

This project was heavily inspired by the incredible work of **Mark Carrington ([@MarkMpn](https://github.com/MarkMpn))** on **[SQL 4 CDS](https://github.com/MarkMpn/Sql4Cds)** and the **[XrmToolBox](https://www.xrmtoolbox.com/)** ecosystem. 

SQL 4 CDS set the standard for querying Microsoft Dataverse / Dynamics 365 using standard SQL syntax. This bookmarklet was created to provide a lightweight, browser-native option for scenarios where installing desktop tools like XrmToolBox is not possible.

---

## Contributing & Reporting Issues

Found a bug or have a suggestion? Please open an issue on the repository. Pull requests are welcome!


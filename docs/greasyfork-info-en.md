SharePoint OS adds a desktop-style interface on top of SharePoint Online. When you open a SharePoint site (`https://*.sharepoint.com/*`), you get a desktop, a start menu, and a taskbar where you can place shortcuts to the folders and files you use every day.

**What it does**

- Place shortcuts on a desktop, grouped into categories with optional color coding, favorites, recently used items, and update badges
- Open folders in movable windows and preview files in place, including a built-in text viewer
- Search across the site, and open ZIP files like folders
- Work with files through the SharePoint REST API: upload (including drag and drop), move, copy, rename, delete, and download
- See how much space a folder uses, and back up or restore your layout and all settings
- Choose from 252 built-in theme presets, and adjust fonts and text size
- Japanese / English UI (the language follows your browser by default, and can be switched in the theme window)
- Motion effects, the 3D view, and the full theme list are off by default (lite mode) and can be switched on in the theme window's feature switches
- Extra modules: a 3D view, a shortcut health check (broken links, access, duplicates), a touch mode for phones and tablets, long-press for right-click menus, and a "welcome back" notice that shows what changed while you were away
- An operation log (up to 500 entries, stored only in your browser) that can undo renames, moves, copies, and deletions made through this UI

**Requirements**

- A userscript manager such as Tampermonkey
- Access to a SharePoint Online site. Everything runs with your own SharePoint permissions; the script cannot show or change anything your account cannot already access

**Privacy**

Settings, layouts, and the operation log are stored in your browser's localStorage. The script communicates with your own SharePoint tenant (and your personal OneDrive on the same tenant) and does not send your data to the author or to third-party servers.

**Notes**

- The main script loads two data files (published separately on Greasy Fork as libraries) via @require (about 2.2 MB in total).
- One menu item, "Check the latest dated sheet," works for Excel workbooks (`.xlsx` / `.xlsm`). By default all workbooks are covered; you can narrow it to workbooks whose name contains a keyword of your choice, in the theme window's feature switches.

**Author:** kycodeclaude
**License:** MIT
**Source code:** https://github.com/kycodeclaude/sharepoint-os-shortcut-ui
**Support / donations:** ☕ Ko-fi: https://ko-fi.com/kycodeclaude

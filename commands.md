# WhatsApp Command Syntax for n8n Google Drive Bot

## Overview
These commands can be sent to the connected WhatsApp number to perform actions on Google Drive via n8n.

---

## 1. LIST Command
**Description:** Lists all files in the specified folder.

**Format:**
```
LIST <FolderName>
```
**Example:**
```
LIST ProjectX
```
---

## 2. DELETE Command
**Description:** Deletes a specific file from a given folder. 

**Format:**
```
DELETE <FileName>
```
**Example:**
```
DELETE report.pdf
```

---

## 3. MOVE Command
**Description:** Moves a file from one folder to a dummy folder.

**Format:**
```
MOVE <FileName> 
```
**Example:**
```
MOVE report.pdf
```

---

## 4. SUMMARY Command
**Description:** Summarizes the contents of a file. Supported file types: PDF, DOCX, TXT.

**Format:**
```
SUMMARISE <FileName>
```
**Example:**
```
SUMMARISE report.pdf
```


---

## Notes
- Folder and file names are **case-sensitive**.
- Only works within the authenticated Google Drive account.
- Ensure proper permissions are granted to the n8n workflow.

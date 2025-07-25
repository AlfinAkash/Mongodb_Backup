#  MongoDB Backup & Export Guide

## 🛠 Prerequisite: Install MongoDB Database Tools

Before using the commands below, download and install the **MongoDB Database Tools** from the official source:

 [Download MongoDB Database Tools](https://www.mongodb.com/try/download/database-tools)

---

##  Export Collection to JSON

Use `mongoexport` to export a specific collection to a JSON file:

```bash
mongoexport --uri="your_connection_string" --collection=yourCollection --out=data.json
```

>  Replace `your_connection_string` and `yourCollection` with actual values.

---

##  Backup Entire Database (BSON Format)

Use `mongodump` to take a full backup of a database in BSON format:

```bash
mongodump --uri="mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<dbname>?retryWrites=true&w=majority&appName=<appname>" --out=<foldername>
```

- `<username>`: Your MongoDB username  
- `<password>`: Your MongoDB password  
- `<cluster>`: Your cluster name (e.g., kac)  
- `<dbname>`: Name of the database (e.g., KAC1)  
- `<appname>`: Application name in your connection string  
- `<foldername>`: Folder where the BSON files will be saved  

---

##  Convert BSON to JSON (Windows CMD)

After taking a backup using `mongodump`, use this command to convert all `.bson` files in a folder to `.json`:

> Make sure you're in the folder containing `.bson` files (e.g., `cd KAC1_backup/KAC1`)

```cmd
for %f in (*.bson) do bsondump "%f" > "%~nf.json"
```

If using in a batch file (`.bat`), **double the `%` signs**:

```bat
for %%f in (*.bson) do bsondump "%%f" > "%%~nf.json"
```

---

##  Example Workflow

```bash
# 1. Dump MongoDB data to BSON files
mongodump --uri="mongodb+srv://user:pass@cluster.mongodb.net/myDB?retryWrites=true&w=majority&appName=App" --out=backup

# 2. Go into the BSON folder
cd backup/myDB

# 3. Convert all BSON files to JSON
for %f in (*.bson) do bsondump "%f" > "%~nf.json"
```

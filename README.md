# Patient Information System

> A standalone desktop application for managing patient medical records with no external dependencies

## What is this?

A Python/Tkinter GUI application that lets healthcare practitioners manage patient records locally. Create, update, search, display, and delete patient information—all stored in a local SQLite database. Zero configuration, zero external dependencies, just run and go.

## Install

Requires Python 3.6+ with Tkinter (included by default on most systems).

```bash
git clone https://github.com/ptanmay143/patient-information-system.git
cd patient-information-system
python patient-information-system.py
```

That's it. The database file (`dbFile.db`) is created automatically on first run.

**Verify Tkinter is available:**
```bash
python -m tkinter
```

## Usage

The application opens with six operation buttons:

**Adding a Patient Record:**

1. Click **Insert**
2. Fill in patient details (ID, name, DOB, contact info, medical history)
3. Click **Insert** to save

All fields are validated on insert:
- Patient ID: exactly 3 digits
- First/Last Name: alphabetic only (no spaces or numbers)
- Phone: exactly 10 digits
- Email: must contain @ and at least one period
- Medical History: alphabetic only (no spaces, numbers, or special characters)
- Doctor Name: alphabetic only (no spaces or numbers)

**Updating Records:**

1. Click **Update**
2. Enter patient ID
3. Edit any fields
4. Click **Update** to save

**Searching Records:**

1. Click **Search**
2. Enter patient ID
3. View matching results in table

**Viewing All Records:**

Click **Display** to see all patient records in a table.

**Deleting Records:**

1. Click **Delete**
2. Enter patient ID
3. Record is deleted immediately (no confirmation)

## API

This is a GUI application without a programmatic API. All interaction is through the Tkinter interface.

The code is organized into these classes:

- `Database` - SQLite connection and CRUD operations
- `Values` - Input validation (used only for insert operations)
- `InsertWindow` - GUI for creating new records
- `UpdateWindow` - GUI for editing existing records  
- `SearchDeleteWindow` - GUI for search and delete operations
- `DatabaseView` - Display window showing all records in table format

Patient records include: ID, first/last name, date of birth, gender, address, phone, email, blood group, medical history, and assigned doctor.

## Known Limitations

- **No update validation** - Update operation bypasses all field validation
- **No delete confirmation** - Records deleted immediately without warning
- **Duplicate IDs possible** - Database schema has typo ("PRIMARYKEY" as one word instead of "PRIMARY KEY"), so IDs are not actually unique
- **Text-only storage** - All fields stored as TEXT type in SQLite
- **Strict validation** - Insert requires alphabetic-only fields for names/history/doctor (no spaces allowed, which prevents entries like "Dr. Smith" or "diabetes type 2")
- **Single-file monolith** - Entire app in one 700+ line file
- **No error handling** - Database errors fail silently

These are documented design choices of the current implementation. Pull requests welcome!

## Creating Standalone Executables

Bundle as a standalone executable using PyInstaller:

```bash
pip install pyinstaller
pyinstaller --onefile --windowed patient-information-system.py
```

Executable will be in `dist/` directory.

## Contributing

Pull requests welcome! For major changes, please open an issue first.

1. Fork this repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Test your changes (`python patient-information-system.py`)
4. Commit your changes (`git commit -m 'Add amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request

## License

[MIT](LICENSE)

# Patient Information System

## Project Title

Patient Information System

## Overview

A desktop graphical user interface (GUI) application for managing patient medical records. Built with Python's standard library, the system enables healthcare practitioners to perform complete CRUD (Create, Read, Update, Delete) operations on patient records stored in a local SQLite database. No external network or dependencies required beyond Python's built-in libraries.

## Architecture Overview

The application follows a three-layer architecture:

```
┌─────────────────────────────────────┐
│       Tkinter GUI Layer             │
│  (Multiple windows for CRUD flows)  │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│    Validation Layer                 │
│    (Values.Validate class)          │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  Database Layer (SQLite3)           │
│  (Database class with CRUD methods) │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│     dbFile.db (File-based storage)  │
│     patient_info table              │
└─────────────────────────────────────┘
```

**Components:**
- **Tkinter UI Layer**: Multi-window interface with separate windows for Insert, Update, Search, Display, and Delete workflows
- **Validation Layer**: Field validation for insert operations (excludes update operations)
- **Database Layer**: SQLite3 wrapper providing abstraction for CRUD operations
- **Persistence Layer**: Local SQLite database file (auto-created on first run)

## Installation and Setup

### Prerequisites

- Python 3.6 or higher
- Tkinter (included with Python on Windows and Linux; use `python -m tkinter` to verify)
- SQLite3 (included with Python standard library)

### Steps

1. Clone or download the repository:
   ```bash
   git clone https://github.com/ptanmay143/patient-information-system.git
   cd patient-information-system
   ```

2. Verify Python and Tkinter installation:
   ```bash
   python --version
   python -m tkinter
   ```
   A small Tkinter window should appear, confirming installation.

3. Run the application:
   ```bash
   python patient-information-system.py
   ```

The application window opens immediately. The SQLite database file (dbFile.db) is automatically created in the working directory on first run.

## Configuration

The application uses hard-coded configuration with no external configuration files. All settings are defined in the source code:

- **Database Location**: `dbFile.db` in the current working directory (line 7 of patient-information-system.py)
- **Database Table**: `patient_info` created with 13 columns
- **Validation Rules**: Hard-coded in the `Values.Validate()` method
- **UI Layout**: Fixed Tkinter window with buttons for each operation

To modify configuration, edit the Python source directly:
- Change database path: Edit `self.dbConnection = sqlite3.connect("dbFile.db")`
- Change table schema: Edit the `CREATE TABLE` statement
- Change validation rules: Edit the `Values.Validate()` method

## Usage

### Main Menu

The home page displays six buttons for operations:

1. **Insert** - Create new patient record
2. **Update** - Modify existing patient record
3. **Search** - Look up patient by ID
4. **Display** - View all records in table format
5. **Delete** - Remove patient record
6. **Exit** - Close application

### Insert Workflow

1. Click "Insert" button
2. Fill in all required fields:
   - Patient ID (3-digit number, numeric only)
   - First Name (alphabetic characters only)
   - Last Name (alphabetic characters only)
   - Date of Birth (day, month, year via dropdown menus)
   - Gender (dropdown: Male, Female, Transgender, Other)
   - Address (free text)
   - Phone Number (10-digit number)
   - Email (must contain @ and .)
   - Blood Group (dropdown: A+, A-, B+, B-, O+, O-, AB+, AB-)
   - Medical History (alphabetic characters only)
   - Doctor Name (alphabetic characters only)
3. Click "Insert" to save, "Reset" to clear fields, or "Close" to cancel
4. Validation errors appear in a message dialog

### Update Workflow

1. Click "Update" button
2. Enter patient ID to modify
3. New window displays current values in editable fields
4. Modify fields as needed
5. Click "Update" to commit or "Close" to cancel
6. Note: Update operation does NOT validate input

### Search Workflow

1. Click "Search" button
2. Enter patient ID
3. Matching record(s) display in table view

### Delete Workflow

1. Click "Delete" button
2. Enter patient ID
3. Record is immediately deleted (no confirmation)

### Display Workflow

1. Click "Display" button
2. All records appear in table view

## Dependencies

All dependencies are from Python's standard library:

| Module | Purpose |
|--------|---------|
| `tkinter` | GUI framework and widgets |
| `tkinter.ttk` | Themed widgets (Combobox) |
| `tkinter.messagebox` | Dialog boxes for validation errors |
| `sqlite3` | SQL database engine |

No third-party packages required.

## Development and Testing

### Current Code Organization

The entire application is implemented in a single 711-line Python file containing three main classes:

- **Database**: SQLite connection and CRUD method wrappers
- **Values**: Input validation logic (used only for Insert workflow)
- **InsertWindow** and other window classes: GUI construction and event handling

### Code Quality Observations

- Single-file monolithic structure (no modularization)
- Inconsistent naming conventions (mix of camelCase and snake_case)
- Validation applied only to Insert operations (Update accepts any input)
- Multiple root Tkinter windows instead of proper dialog handling
- No error handling around database operations
- No logging or debugging support
- No automated tests

### Testing

No automated test suite exists. Manual testing approach only:

1. Test Insert with valid/invalid inputs
2. Test each CRUD operation with various data
3. Test database persistence by restarting application

Recommended test framework: `pytest` or `unittest` (both available in Python standard library).

## Deployment

Designed for single-user local desktop environments with no network requirements.

### Local Execution

```bash
python patient-information-system.py
```

### Bundled Executable (PyInstaller)

Create a standalone executable for distribution:

```bash
pip install pyinstaller
pyinstaller --onefile --windowed patient-information-system.py
```

Output: `dist/patient-information-system.exe` (Windows) or equivalent binary.

### System Requirements for Deployment

- Python 3.6+ OR bundled PyInstaller executable
- Operating System: Windows, macOS, or Linux with Tkinter support
- Disk Space: ~5 MB (application) + data usage (typically small)
- RAM: ~50 MB

## Limitations and Future Improvements

### Limitations

| Issue | Impact | Severity |
|-------|--------|----------|
| No validation on Update operation | Users can insert invalid data | High |
| All columns stored as TEXT | No type constraints or indexes | High |
| No primary key constraint | Duplicate patient IDs possible | High |
| No confirmation for Delete | Accidental data loss possible | High |
| Silent database failures | Users unaware of errors | Medium |
| Window stacking issues | Multiple root windows confusing | Medium |
| No transaction support | Partial failures possible | Medium |
| Single-file monolithic code | Unmaintainable for large systems | Low |
| No rollback capability | No undo for operations | Low |

### Future Improvements

1. Add proper database schema with PRIMARY KEY, type constraints, and UNIQUE constraints
2. Implement confirmation dialogs for destructive operations (Delete)
3. Add validation to Update operation (currently accepts any input)
4. Validate phone numbers with regex pattern
5. Validate email format with regex
6. Store dates as proper DATE type instead of separate year/month/day fields
7. Implement multi-field search (not just ID)
8. Add CSV export/import functionality
9. Implement audit logging for all changes
10. Add role-based access control for multi-user deployments
11. Implement proper exception handling with user-facing error messages
12. Add unit tests with pytest or unittest
13. Create separate modules (db.py, ui.py, validation.py)
14. Add database connection pooling
15. Consider web-based interface with Flask or Django

## Contribution Guidelines

1. Fork the repository on GitHub
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make focused changes addressing a single concern
4. Verify the application runs: `python patient-information-system.py`
5. Add test coverage for new functionality
6. Commit with clear messages: `git commit -m "Add feature: description"`
7. Push to your branch: `git push origin feature/your-feature-name`
8. Submit a pull request with description of changes

## License

MIT License - See [LICENSE](LICENSE) file for complete terms.

Permission is granted to use, modify, and distribute this software for any purpose, provided the license and copyright notice are included.

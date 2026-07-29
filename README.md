<h1 align="center">
  <a href="https://github.com/ptanmay143/patient-information-system">
    <img src="docs/images/logo.svg" alt="Logo" width="100" height="100">
  </a>
</h1>

<div align="center">
  Patient Information System
  <br />
  <a href="#about"><strong>Explore the screenshots »</strong></a>
  <br />
  <br />
  <a href="https://github.com/ptanmay143/patient-information-system/issues/new?assignees=&labels=bug&template=01_BUG_REPORT.md&title=bug%3A+">Report a Bug</a>
  ·
  <a href="https://github.com/ptanmay143/patient-information-system/issues/new?assignees=&labels=enhancement&template=02_FEATURE_REQUEST.md&title=feat%3A+">Request a Feature</a>
  ·
  <a href="https://github.com/ptanmay143/patient-information-system/issues/new?assignees=&labels=question&template=04_SUPPORT_QUESTION.md&title=support%3A+">Ask a Question</a>
</div>

<div align="center">
<br />

[![Project license](https://img.shields.io/github/license/ptanmay143/patient-information-system.svg?style=flat-square)](LICENSE)
[![Pull Requests welcome](https://img.shields.io/badge/PRs-welcome-ff69b4.svg?style=flat-square)](https://github.com/ptanmay143/patient-information-system/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22)
[![code with love by ptanmay143](https://img.shields.io/badge/%3C%2F%3E%20with%20%E2%99%A5%20by-ptanmay143-ff1414.svg?style=flat-square)](https://github.com/ptanmay143)

</div>

<details open="open">
<summary>Table of Contents</summary>

- [About](#about)
  - [Built With](#built-with)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Roadmap](#roadmap)
- [Support](#support)
- [Project Assistance](#project-assistance)
- [Contributing](#contributing)
- [Authors & contributors](#authors--contributors)
- [Security](#security)
- [License](#license)
- [Acknowledgements](#acknowledgements)

</details>

---

## About

Patient Information System is a desktop medical-record utility for clinics and individual practitioners who need a lightweight local registry without setting up a web server or external database. It provides a Tkinter user interface for adding, updating, searching, deleting, and listing patient records while persisting data in a local SQLite file.

The project is designed for simple environments where low setup effort matters more than distributed architecture. On first launch, the application creates `dbFile.db` automatically and builds a `patient_info` table if it does not already exist, so a developer or operator can begin data entry immediately.

Functionally, the app is organized around distinct windows that map to operational tasks: `InsertWindow`, `UpdateWindow`, `SearchDeleteWindow`, and `DatabaseView`, all started from `HomePage`. A `Database` class handles CRUD calls and a `Values` validator enforces insertion constraints such as ID, phone, and email formats.

The current design intentionally favors single-file simplicity and standard-library-only dependencies (`tkinter`, `sqlite3`) over modularity. That keeps onboarding easy but also means important constraints should be understood upfront: insertion validates fields but updates do not, deletion has no confirmation prompt, and table schema typing is broad (`text`) across all columns.

<details>
<summary>Screenshots</summary>
<br>

This project has a graphical interface. Add screenshots under `docs/images/` and reference them here.

|                               Home Page                               |                               Insert Window                               |
| :-------------------------------------------------------------------: | :-----------------------------------------------------------------------: |
| <img src="docs/images/screenshot.png" title="Home Page" width="100%"> | <img src="docs/images/screenshot.png" title="Insert Window" width="100%"> |

</details>

### Built With

- **Python 3** — runtime for the GUI and local data handling.
- **Tkinter / tkinter.ttk / tkinter.messagebox** — native desktop interface toolkit and dialog widgets.
- **SQLite (`sqlite3`)** — embedded local database for patient storage.

---

## Getting Started

Setup is straightforward and typically takes a few minutes: clone, verify Python/Tkinter availability, and run the script. No external services, package manager bootstrap, or migration framework is required.

### Prerequisites

- **Python 3.6+** — install from [python.org](https://www.python.org/downloads/). The project uses modern Python 3 syntax and standard library modules.
- **Tkinter support in Python** — usually bundled with official Python installers. Validate with:
  ```bash
  python -m tkinter
  ```

### Installation

1. Clone the repository.

```bash
git clone https://github.com/ptanmay143/patient-information-system.git
```

1. Move into the project directory.

```bash
cd patient-information-system
```

1. Start the desktop application.

```bash
python patient-information-system.py
```

1. Verify successful startup.

```text
Expected result: a Tkinter window titled "Patient Information System" opens with
buttons for Insert, Update, Search, Delete, Display, and Exit.
```

1. Optional: build a standalone executable.

```bash
pip install pyinstaller
pyinstaller --onefile --windowed patient-information-system.py
```

### Environment Variables

This project does not read environment variables.

| Variable | Required | Default | Description                                      | Example Value |
| -------- | -------- | ------- | ------------------------------------------------ | ------------- |
| None     | No       | N/A     | Desktop app uses hard-coded local configuration. | N/A           |

---

## Usage

Run the application:

```bash
python patient-information-system.py
```

Primary user flow:

1. Click **Insert** to create a new patient record.
1. Complete fields including patient ID, personal details, contact details, blood group, history, and doctor.
1. Click **Insert** to persist to SQLite.

Insert-time validation rules enforced by `Values.Validate`:

- Patient ID must be exactly 3 digits.
- First and last names must be alphabetic.
- Phone must be exactly 10 digits.
- Email must contain one `@` and at least one `.`.
- History and doctor fields must be alphabetic.

Other operational commands:

- **Update** — prompts for ID, shows existing row, writes edited values using SQL `UPDATE`.
- **Search** — prompts for ID and opens a table view for matching records.
- **Display** — opens a table with all rows from `patient_info`.
- **Delete** — prompts for ID and deletes immediately with no confirmation dialog.

Data flow summary:

```text
Tkinter Window -> User Input -> Database class SQL call -> SQLite dbFile.db
```

Runtime behavior to know:

- `dbFile.db` is created in the project root on first run.
- The table definition uses `id PRIMARYKEY text`, so uniqueness enforcement on `id` is not guaranteed.
- Update and delete actions do not currently include the same strict guardrails as insert.

This is a desktop GUI application and does not expose HTTP endpoints.

---

## Roadmap

See the [open issues](https://github.com/ptanmay143/patient-information-system/issues) for a full list of proposed features and known bugs.

- [Top Feature Requests](https://github.com/ptanmay143/patient-information-system/issues?q=label%3Aenhancement+is%3Aopen+sort%3Areactions-%2B1-desc) (Add your votes using the 👍 reaction)
- [Top Bugs](https://github.com/ptanmay143/patient-information-system/issues?q=is%3Aissue+is%3Aopen+label%3Abug+sort%3Areactions-%2B1-desc) (Add your votes using the 👍 reaction)
- [Newest Bugs](https://github.com/ptanmay143/patient-information-system/issues?q=is%3Aopen+is%3Aissue+label%3Abug)

Planned direction from current code constraints includes schema hardening (`PRIMARY KEY` on ID), update-path validation parity with insert, explicit error handling around DB calls, and safer delete UX with confirmation.

---

## Support

Reach out to the maintainer at one of the following places:

- [GitHub issues](https://github.com/ptanmay143/patient-information-system/issues/new?assignees=&labels=question&template=04_SUPPORT_QUESTION.md&title=support%3A+)
- Contact options listed on [this GitHub profile](https://github.com/ptanmay143)

---

## Project Assistance

If you want to say **thank you** or support active development of Patient Information System:

- Add a [GitHub Star](https://github.com/ptanmay143/patient-information-system) to the project.
- Share the project with peers who need lightweight desktop health-record tooling.
- Write about practical improvements or use cases in your blog or social channels.

Together, we can make Patient Information System **better**!

---

## Contributing

First off, thanks for taking the time to contribute! Contributions are what make the open-source community such an amazing place to learn, inspire, and create.

Recommended workflow:

1. Fork the repository.
1. Create a branch from `master`.
1. Make focused changes and test manually with the GUI.
1. Open a pull request with clear reproduction and validation notes.

No dedicated `docs/CONTRIBUTING.md` exists at this time, so use this repository-level workflow and include local verification steps you used (for example: insert, update, search, delete, display flows).

---

## Authors & Contributors

The original setup of this repository is by [Tanmay Pachpande](https://github.com/ptanmay143).

For a full list of all authors and contributors, see [the contributors page](https://github.com/ptanmay143/patient-information-system/contributors).

---

## Security

Patient Information System follows good practices of security, but 100% security cannot be assured. Patient Information System is provided **"as is"** without any **warranty**. Use at your own risk.

_No dedicated security policy file is currently present in this repository. Use GitHub private vulnerability reporting where possible, or open a security-marked issue without disclosing sensitive exploit details publicly._

---

## License

This project is licensed under the **MIT License**.

See [LICENSE](LICENSE) for more information.

---

## Acknowledgements

- Python core developers and Tk maintainers for the standard GUI/tooling stack.
- SQLite maintainers for the embedded database used by the project.
- Community contributors and testers improving reliability and usability.

<!-- Generated by README_GENERATOR_PROMPT v0.1 -->

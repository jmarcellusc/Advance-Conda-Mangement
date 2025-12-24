# Advanced Conda Management- Application

A Windows-focused utility for **backing up, restoring, repairing, and cleaning Conda environments** with an emphasis on **stability**, **reproducibility**, and **DLL conflict prevention**.

This tool is designed for users who manage **multiple Conda environments**, work with **scientific / GIS / data stacks**, or routinely encounter broken environments caused by solver conflicts, pip failures, or PATH pollution.

**NOTE** Please read: "Disclaimer: Use this tool at your own risk. The author is not responsible for any data loss, system changes, or instability that may result from its use."

---

## File
- **Version 1.1** (_1a.exe) - Status: Active. Disabled yaml installation. Additionally menu item #4 and #6 have not yet been tested in another PC (and might required code generalization). I recommend NOT to use these items and please read the disclaimer noted throughout this information posted.
- **Verion 1.0** - Removed, errors with a dependency: gdk-pixbuf (a common dependency for graphics) includes a post-link script. Will investigate the potential bypass or correct commands. Also disabling libmamba compatibility.

## Key Features

- Portable: all backups and metadata live next to the application or executable
- Safe environment restoration with isolated pip handling
- High-performance dependency solving via **libmamba**
- Registry-level PATH cleanup to prevent DLL collisions
- One-click deep clean for catastrophic Conda failures
- No admin rights required (except where Windows enforces it)

---

## Directory Layout

```
Advanced-Conda-Management-Suite/
├── main.py
├── conda_backups/
│   ├── env1_20250101_1200.yml
│   ├── env2_20250101_1200.yml
│   └── ...
```

When packaged as an executable, all paths resolve relative to the `.exe` location.

---

## Menu Options

### 1. Backup All Environments (Timestamped)

Exports **every detected Conda environment** to YAML files using:

```
conda env export --no-builds
```

- Each environment is saved with a timestamp
- Backups are cross-platform and portable
- Ideal for migration, disaster recovery, or version pinning

---

### 2. Scan and Install via Libmamba

Restores an environment from a YAML file using:

- The **libmamba** dependency solver
- Standard `conda env create` semantics

Best used when:
- The YAML is known to be clean
- Pip usage is minimal
- Fast restores are preferred

---

### 3. Scan and Install via Safe-Sync (PIP)

A **two-phase restore strategy** designed to prevent Conda/Pip conflicts.

**Phase 1**
- Create the environment using Conda only

**Phase 2**
- Install pip dependencies individually using `conda run`

This avoids:
- Solver poisoning
- Partial installs
- Broken shared libraries

Recommended for:
- Mixed Conda + Pip environments
- GIS, ML, and scientific stacks
- Historically fragile environments

---

### 4. AUTO-CLEAN Windows User PATH (Registry)
**Disclaimer: Use this tool at your own risk. The author is not responsible for any data loss, system changes, or instability that may result from its use.**

Removes **Anaconda / Miniconda paths** from the Windows **User PATH** registry key:

```
HKEY_CURRENT_USER\Environment
```

Purpose:
- Prevent DLL collisions
- Stop Conda from hijacking system Python
- Eliminate crashes in unrelated software

 Does **not** uninstall Conda  
 Requires restarting terminals to take effect  

This enforces **explicit environment activation**.

---

### 5. Conda Command Reference (Cheat Sheet)

Displays an extended reference covering:

- Environment management
- Solver and channel configuration
- Cleanup and diagnostics
- Pip interoperability

Useful as:
- A refresher
- A troubleshooting guide
- A learning aid for advanced Conda usage

---

### 6. EXECUTE: Deep Clean & System Scrub

 **DESTRUCTIVE OPERATION**
**Disclaimer: Use this tool at your own risk. The author is not responsible for any data loss, system changes, or instability that may result from its use.**
Performs a **full Conda reset**:

- Terminates locking Python / Conda processes
- Runs `anaconda-clean`
- Deletes Conda directories
- Scrubs PATH registry entries

Use **only** when:
- Conda is irreparably broken
- DLL conflicts persist after standard cleanup
- A full reinstall is required

A system reboot is required afterward.

---

## Intended Audience

This tool is intended for:

- Data scientists
- GIS professionals
- Scientific Python users
- Developers managing multiple Conda stacks
- Anyone tired of reinstalling Conda repeatedly

Basic familiarity with Conda is assumed.

---

## Disclaimer

This tool modifies:
- Conda environments
- Local filesystem state
- Windows user registry keys

Use at your own risk.  
Always back up critical environments before performing destructive operations.

---

## License

MIT License

* 2025 Juan Marcel Campos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


# Anaconda, Conda & VS Code — Complete Setup and Recovery Guide

> **Purpose:** This document explains how to configure, start, use and troubleshoot Anaconda, Conda, Python, VS Code, Git Bash, PowerShell, Command Prompt and Jupyter Notebook on Windows.
>
> It is designed as a long-term reference so that configuration problems can be diagnosed and fixed without reinstalling Anaconda.

---

# 1. System Configuration — Verified Setup

The following configuration was verified on 8 November 2026.

| Setting | Verified value |
|:---|:---|
| Project name | `uk-housing-data-pipeline` |
| Windows username | `imksa` |
| Anaconda distribution | Anaconda |
| Anaconda installation | `C:\Users\imksa\anaconda3` |
| Conda environment | `uk-housing-env` |
| Python version | `3.12.16` |
| Project directory | `C:\Users\imksa\Desktop\PROJECTS\uk-housing-data-pipeline` |
| Git Bash shell | `/usr/bin/bash` |
| Git Bash home | `/c/Users/imksa` |
| Jupyter kernel | `Python (uk-housing-env)` |
| Operating system | Windows |
| IDE | Visual Studio Code |
| Version control | Git and GitHub |

## 1.1 Important installation paths

| Component | Windows path |
|:---|:---|
| Anaconda root | `C:\Users\imksa\anaconda3` |
| Conda executable | `C:\Users\imksa\anaconda3\Scripts\conda.exe` |
| Conda command wrapper | `C:\Users\imksa\anaconda3\condabin\conda.bat` |
| Conda PowerShell hook | `C:\Users\imksa\anaconda3\shell\condabin\conda-hook.ps1` |
| Conda Bash script | `C:\Users\imksa\anaconda3\etc\profile.d\conda.sh` |
| Base Python | `C:\Users\imksa\anaconda3\python.exe` |
| Project environment | `C:\Users\imksa\anaconda3\envs\uk-housing-env` |
| Project Python | `C:\Users\imksa\anaconda3\envs\uk-housing-env\python.exe` |

## 1.2 Project folder structure

Recommended structure:

```text
uk-housing-data-pipeline/
│
├── .git/
├── .gitignore
├── README.md
├── environment.yml
│
├── docs/
│   └── CONDA_VSCODE_SETUP_AND_RECOVERY.md
│
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
│
├── notebooks/
│
├── src/
│
├── outputs/
│
├── reports/
│
└── requirements.txt
```

**Important:** Do not put the entire Anaconda installation or Conda environment inside the Git repository. Keep the environment outside the project directory.

---

# 2. Understanding Anaconda, Conda and Python

| Component | Explanation | Purpose |
|:---|:---|:---|
| Anaconda | Python distribution | Provides Python, Conda and data science tools |
| Conda | Environment and package manager | Creates environments and installs packages |
| Python | Programming language | Runs scripts, notebooks and applications |
| Conda environment | Isolated Python installation | Keeps project dependencies separate |
| VS Code | Code editor | Used for Python development |
| Python interpreter | Selected Python executable | Determines which Python VS Code uses |
| Jupyter Notebook | Interactive coding environment | Runs code in notebook cells |
| Jupyter kernel | Python process for notebooks | Connects notebooks to a particular environment |
| Git | Version control system | Tracks project changes |
| GitHub | Online Git repository hosting | Stores and shares project code |

## 2.1 How everything connects

```text
Windows
   │
   ├── Anaconda
   │      │
   │      └── Conda
   │             │
   │             └── uk-housing-env
   │                    │
   │                    └── Python 3.12.16
   │
   ├── PowerShell
   │
   ├── Command Prompt
   │
   ├── Git Bash
   │
   └── Visual Studio Code
          │
          ├── Python Interpreter
          │       └── uk-housing-env
          │
          └── Jupyter Notebook
                  └── Python (uk-housing-env)
```

**Important distinction:**

- Terminal activation controls the Python environment available to that terminal.
- VS Code interpreter selection controls which Python VS Code uses for running Python files and related features.
- Jupyter kernel selection controls which Python environment executes notebook cells.

These three settings should point to the same project environment.

---

# 3. Daily Startup Workflow

You do not need to reinstall or reconfigure Conda every time you start working.

Once the shell is configured, simply activate the existing environment.

## 3.1 Option A — Start from Anaconda Prompt

| Step | Action | Command |
|:---:|:---|:---|
| 1 | Open Anaconda Prompt | Windows Start Menu |
| 2 | Activate project environment | `conda activate uk-housing-env` |
| 3 | Navigate to project | `cd /d C:\Users\imksa\Desktop\PROJECTS\uk-housing-data-pipeline` |
| 4 | Open VS Code | `code .` |

## 3.2 Option B — Start from PowerShell

| Step | Action | Command |
|:---:|:---|:---|
| 1 | Open PowerShell | Windows Start Menu |
| 2 | Navigate to project | `cd C:\Users\imksa\Desktop\PROJECTS\uk-housing-data-pipeline` |
| 3 | Activate environment | `conda activate uk-housing-env` |
| 4 | Verify Python | `python --version` |
| 5 | Open VS Code if required | `code .` |

## 3.3 Option C — Start from Command Prompt

| Step | Action | Command |
|:---:|:---|:---|
| 1 | Open CMD | Windows Start Menu |
| 2 | Navigate to project | `cd /d C:\Users\imksa\Desktop\PROJECTS\uk-housing-data-pipeline` |
| 3 | Activate environment | `conda activate uk-housing-env` |
| 4 | Verify Python | `python --version` |
| 5 | Open VS Code | `code .` |

## 3.4 Option D — Start from Git Bash

| Step | Action | Command |
|:---:|:---|:---|
| 1 | Open Git Bash | VS Code terminal or Git Bash application |
| 2 | Navigate to project | `cd ~/Desktop/PROJECTS/uk-housing-data-pipeline` |
| 3 | Activate environment | `conda activate uk-housing-env` |
| 4 | Verify Python | `python --version` |
| 5 | Verify executable | `which python` |

**Expected terminal prompt:**

```text
(uk-housing-env) imksa@imksav ...
```

The `(uk-housing-env)` prefix confirms that the environment is activated.

---

# 4. Conda Configuration for All Terminals

Conda needs shell-specific initialisation because PowerShell, CMD and Bash work differently.

| Terminal | Initialisation command | Startup configuration |
|:---|:---|:---|
| Anaconda Prompt | Already configured by Anaconda | Anaconda Prompt activation scripts |
| PowerShell | `conda init powershell` | PowerShell profile |
| Command Prompt | `conda init cmd.exe` | CMD AutoRun configuration |
| Git Bash | `conda init bash` or manual Bash setup | `.bash_profile` / `.bashrc` |

**Important:** Run initialisation commands from Anaconda Prompt whenever possible.

## 4.1 PowerShell initialisation

Open Anaconda Prompt and execute:

```cmd
conda init powershell
```

Close existing PowerShell terminals and open a new one.

Test:

```powershell
conda --version
conda activate uk-housing-env
python --version
```

Expected:

```text
(uk-housing-env) PS C:\Users\imksa>
Python 3.12.16
```

## 4.2 Command Prompt initialisation

Open Anaconda Prompt:

```cmd
conda init cmd.exe
```

Close and reopen Command Prompt.

Test:

```cmd
conda --version
conda activate uk-housing-env
python --version
```

Expected:

```text
(uk-housing-env) C:\Users\imksa>
Python 3.12.16
```

## 4.3 Git Bash initialisation

Git Bash requires its Bash startup files to load Conda.

The verified working arrangement for this computer is:

| File | Responsibility |
|:---|:---|
| `~/.bash_profile` | Loads `.bashrc` when Bash starts as a login shell |
| `~/.bashrc` | Loads the Anaconda Conda initialisation script |
| `conda.sh` | Enables Conda commands and activation |

### Step 1 — Check Git Bash configuration

```bash
echo $SHELL
echo $HOME
```

Expected:

```text
/usr/bin/bash
/c/Users/imksa
```

### Step 2 — Configure `.bash_profile`

Location:

```text
C:\Users\imksa\.bash_profile
```

Contents:

```bash
# Load Bash configuration
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

### Step 3 — Configure `.bashrc`

Location:

```text
C:\Users\imksa\.bashrc
```

Contents:

```bash
# Initialise Anaconda Conda
if [ -f "/c/Users/imksa/anaconda3/etc/profile.d/conda.sh" ]; then
    source "/c/Users/imksa/anaconda3/etc/profile.d/conda.sh"
fi
```

### Step 4 — Restart Git Bash

Close all Git Bash terminal sessions.

Open a new Git Bash terminal and execute:

```bash
conda --version
```

Then:

```bash
conda activate uk-housing-env
```

Verify:

```bash
python --version
which python
```

Expected:

```text
Python 3.12.16
/c/Users/imksa/anaconda3/envs/uk-housing-env/python
```

**Important:** The above arrangement uses one Conda initialisation route through `.bashrc`. Avoid duplicating the Conda hook in both files.

---

# 5. Windows PATH Configuration

Windows PATH tells the operating system where to find executable programs.

A PATH configuration issue can prevent Conda or PowerShell from being recognised.

## 5.1 Recommended Anaconda PATH entries

| PATH entry | Purpose |
|:---|:---|
| `C:\Users\imksa\anaconda3` | Anaconda installation |
| `C:\Users\imksa\anaconda3\Scripts` | Conda and Python scripts |
| `C:\Users\imksa\anaconda3\condabin` | Conda command wrappers |

## 5.2 Windows system PATH entries

| PATH entry | Purpose |
|:---|:---|
| `C:\Windows\System32` | Windows system utilities |
| `C:\Windows` | Windows system directory |
| `C:\Windows\System32\Wbem` | Windows management utilities |
| `C:\Windows\System32\WindowsPowerShell\v1.0\` | Windows PowerShell |

**Warning:** Do not delete existing Windows PATH entries. Only add missing entries.

Also, do not add the `uk-housing-env` Python directory globally. Conda manages the environment-specific Python PATH during activation.

## 5.3 How to edit Windows PATH

| Step | Instruction |
|:---:|:---|
| 1 | Press `Win + R` |
| 2 | Type `sysdm.cpl` |
| 3 | Open the Advanced tab |
| 4 | Select Environment Variables |
| 5 | Find the Path variable under User variables |
| 6 | Select Edit |
| 7 | Add only missing paths |
| 8 | Save all changes |
| 9 | Restart terminals and VS Code |

## 5.4 Verify PATH from Command Prompt

```cmd
where.exe conda
where.exe python
where.exe powershell
```

Expected PowerShell path:

```text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

Expected Conda paths may include:

```text
C:\Users\imksa\anaconda3\Scripts\conda.exe
C:\Users\imksa\anaconda3\condabin\conda.bat
```

---

# 6. VS Code Python Interpreter Configuration

The Python interpreter must point to the project's Conda environment.

## 6.1 Select the interpreter

| Step | Action |
|:---:|:---|
| 1 | Open VS Code |
| 2 | Open `uk-housing-data-pipeline` |
| 3 | Press `Ctrl + Shift + P` |
| 4 | Search for `Python: Select Interpreter` |
| 5 | Select the project environment |
| 6 | If unavailable, select Enter interpreter path |
| 7 | Browse to the Python executable |

Correct interpreter:

```text
C:\Users\imksa\anaconda3\envs\uk-housing-env\python.exe
```

## 6.2 Verify the selected interpreter

Open the VS Code terminal:

```powershell
python --version
```

Then:

```powershell
python -c "import sys; print(sys.executable)"
```

Expected:

```text
C:\Users\imksa\anaconda3\envs\uk-housing-env\python.exe
```

## 6.3 If the interpreter is missing

| Step | Action |
|:---:|:---|
| 1 | Confirm the environment exists using `conda env list` |
| 2 | Activate it in the terminal |
| 3 | Check that its Python executable exists |
| 4 | Use Python: Select Interpreter |
| 5 | Enter the interpreter path manually |
| 6 | Run Developer: Reload Window |

---

# 7. Jupyter Notebook and Kernel Configuration

The Jupyter kernel determines which Python environment executes notebook cells.

## 7.1 Install Jupyter and IPython kernel

Activate the environment:

```powershell
conda activate uk-housing-env
```

Install required packages:

```powershell
conda install jupyter ipykernel -y
```

## 7.2 Register the environment as a kernel

```powershell
python -m ipykernel install --user --name uk-housing-env --display-name "Python (uk-housing-env)"
```

Expected:

```text
Installed kernelspec uk-housing-env
```

## 7.3 Check registered kernels

```powershell
jupyter kernelspec list
```

Expected list includes:

```text
Available kernels:
  python3
  ml-fast-track
  uk-housing-env
```

The exact list may contain additional kernels.

## 7.4 Select the kernel in VS Code

| Step | Action |
|:---:|:---|
| 1 | Open your `.ipynb` file |
| 2 | Click Select Kernel |
| 3 | Choose Select Another Kernel if needed |
| 4 | Choose Jupyter Kernel |
| 5 | Select `Python (uk-housing-env)` |

## 7.5 Verify the notebook kernel

Run:

```python
import sys

print("Python version:", sys.version)
print("Python executable:", sys.executable)
```

Expected executable:

```text
C:\Users\imksa\anaconda3\envs\uk-housing-env\python.exe
```

## 7.6 If the kernel does not appear

| Problem | Solution |
|:---|:---|
| Kernel not registered | Run the `ipykernel install` command again |
| Kernel list is outdated | Reload VS Code |
| Jupyter package missing | Install Jupyter in `uk-housing-env` |
| Wrong Python executable | Select the correct kernel |
| Kernel starts but imports fail | Check that packages are installed in `uk-housing-env` |

---

# 8. Conda Environment Management

A separate environment keeps project packages independent.

## 8.1 Common Conda commands

| Task | Command |
|:---|:---|
| Check Conda version | `conda --version` |
| Display Conda details | `conda info` |
| List environments | `conda env list` |
| Activate environment | `conda activate uk-housing-env` |
| Deactivate environment | `conda deactivate` |
| List packages | `conda list` |
| Install package | `conda install package-name` |
| Update package | `conda update package-name` |
| Remove package | `conda remove package-name` |
| Update Conda | `conda update -n base -c defaults conda` |

## 8.2 Create a new environment

Only do this if the environment does not already exist.

```cmd
conda create -n uk-housing-env python=3.12 -y
```

Activate:

```cmd
conda activate uk-housing-env
```

Verify:

```cmd
python --version
```

## 8.3 Install Python packages

Use Conda when the required package is available through your configured Conda channels:

```bash
conda install pandas numpy matplotlib seaborn scikit-learn -y
```

Use pip for packages that require it:

```bash
python -m pip install package-name
```

Always activate `uk-housing-env` before installing project packages.

## 8.4 Export environment dependencies

Export the environment:

```bash
conda env export --from-history > environment.yml
```

This records the explicitly requested Conda dependencies rather than every transitive package.

Recreate the environment on another computer:

```bash
conda env create -f environment.yml
```

If the environment already exists, update it:

```bash
conda env update -n uk-housing-env -f environment.yml --prune
```

---

# 9. Troubleshooting — Error and Solution Reference

| Error / Problem | Possible cause | Recommended solution |
|:---|:---|:---|
| `conda is not recognized` | Conda not on PATH or shell not initialised | Check installation and initialise the relevant shell |
| `Run conda init before conda activate` | Activation hook missing | Run `conda init` for that shell and restart it |
| `EnvironmentNameNotFound` | Environment missing or incorrect name | Run `conda env list` |
| `No module named ipykernel` | Kernel package missing | Install `ipykernel` in the project environment |
| `No module named pandas` | Package not installed in active environment | Install pandas after activating the environment |
| Kernel missing in VS Code | Kernel not registered or list stale | Register kernel and reload VS Code |
| Python points to base | Wrong environment or interpreter | Activate/select `uk-housing-env` |
| PowerShell not recognised | Windows PATH problem | Check PowerShell directory in system PATH |
| Git Bash cannot find Conda | Bash startup files not loading Conda | Check `.bash_profile` and `.bashrc` |
| FAST_CWD warning | Git Bash / MSYS runtime issue | Verify Python, then update Git for Windows if needed |
| `code` is not recognised | VS Code command not on PATH | Use VS Code terminal or enable its command-line PATH |
| Packages install but notebook cannot import them | Terminal and notebook use different environments | Select `Python (uk-housing-env)` as notebook kernel |

---

# 10. Detailed Recovery Procedures

## 10.1 Recovery: Conda is not recognised in PowerShell

First check the installation:

```powershell
Test-Path "C:\Users\imksa\anaconda3\Scripts\conda.exe"
```

Expected:

```text
True
```

Load Conda manually for the current session:

```powershell
& "C:\Users\imksa\anaconda3\shell\condabin\conda-hook.ps1"
```

Test:

```powershell
conda --version
conda activate uk-housing-env
```

For permanent configuration, run from Anaconda Prompt:

```cmd
conda init powershell
```

Restart PowerShell.

## 10.2 Recovery: Conda activation fails in CMD

Open Anaconda Prompt:

```cmd
conda init cmd.exe
```

Close CMD completely and reopen it.

Test:

```cmd
conda --version
conda activate uk-housing-env
```

## 10.3 Recovery: Conda is missing in Git Bash

Check:

```bash
echo $HOME
ls -la ~/.bash_profile ~/.bashrc
```

Check the Conda script:

```bash
ls /c/Users/imksa/anaconda3/etc/profile.d/conda.sh
```

Expected:

```text
/c/Users/imksa/anaconda3/etc/profile.d/conda.sh
```

Back up the startup files:

```bash
cp ~/.bash_profile ~/.bash_profile.backup
cp ~/.bashrc ~/.bashrc.backup
```

Restore the configuration from Section 4.3.

Restart Git Bash.

Verify:

```bash
conda --version
conda activate uk-housing-env
python --version
```

## 10.4 Recovery: Environment cannot be found

Check available environments:

```bash
conda env list
```

Expected location:

```text
C:\Users\imksa\anaconda3\envs\uk-housing-env
```

If missing, create it:

```bash
conda create -n uk-housing-env python=3.12 -y
```

Then activate:

```bash
conda activate uk-housing-env
```

Do not recreate the environment if it already exists.

## 10.5 Recovery: Jupyter kernel is missing

Activate the environment:

```bash
conda activate uk-housing-env
```

Install the kernel package:

```bash
conda install ipykernel -y
```

Register again:

```bash
python -m ipykernel install --user --name uk-housing-env --display-name "Python (uk-housing-env)"
```

Verify:

```bash
jupyter kernelspec list
```

Restart VS Code.

## 10.6 Recovery: VS Code selects the wrong Python

| Step | Action |
|:---:|:---|
| 1 | Open Command Palette |
| 2 | Select Python: Select Interpreter |
| 3 | Select Enter interpreter path |
| 4 | Browse to the correct `python.exe` |
| 5 | Select the project environment |
| 6 | Reload VS Code |
| 7 | Verify using `sys.executable` |

Correct path:

```text
C:\Users\imksa\anaconda3\envs\uk-housing-env\python.exe
```

## 10.7 Recovery: Git Bash FAST_CWD warning

Previously encountered warning:

```text
Cygwin WARNING:
Couldn't compute FAST_CWD pointer.
```

This is a Git Bash / MSYS runtime warning and does not automatically mean Conda is broken.

Check:

```bash
conda activate uk-housing-env
python -c "import sys; print(sys.executable)"
pwd
```

| Result | Interpretation |
|:---|:---|
| Python points to `uk-housing-env` | Environment activation succeeded |
| Python points to `base` | Activate the project environment again |
| `pwd` shows an unexpected location | Navigate to the project directory |
| Warning persists | Update Git for Windows and restart Git Bash |

Return to the project:

```bash
cd ~/Desktop/PROJECTS/uk-housing-data-pipeline
```

Do not reinstall Anaconda solely because of this warning.

---

# 11. Project Workflow — Python, Jupyter and Git

This section describes the normal development process after Conda configuration is working.

## 11.1 Start the project

```bash
conda activate uk-housing-env
cd ~/Desktop/PROJECTS/uk-housing-data-pipeline
code .
```

## 11.2 Verify the environment

```bash
python --version
python -c "import sys; print(sys.executable)"
```

## 11.3 Install the main data analysis packages

```bash
conda install pandas numpy matplotlib seaborn scikit-learn jupyter ipykernel -y
```

## 11.4 Test package imports

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import sklearn

print("Pandas:", pd.__version__)
print("NumPy:", np.__version__)
print("Scikit-learn:", sklearn.__version__)
print("Environment verification successful.")
```

## 11.5 Export environment configuration

```bash
conda env export --from-history > environment.yml
```

## 11.6 Git status

```bash
git status
```

## 11.7 Add and commit project changes

```bash
git add .
git commit -m "Configure project environment and data analysis workflow"
```

## 11.8 Push to GitHub

```bash
git push origin master
```

If your GitHub branch is `main` instead of `master`, use:

```bash
git push origin main
```

Check the current branch:

```bash
git branch --show-current
```

---

# 12. Git and GitHub Command Reference

| Task | Command |
|:---|:---|
| Check Git version | `git --version` |
| Check current branch | `git branch --show-current` |
| Check working tree | `git status` |
| View recent commits | `git log --oneline -5` |
| Stage all changes | `git add .` |
| Stage one file | `git add filename` |
| Commit changes | `git commit -m "Commit message"` |
| Push current branch | `git push` |
| Pull latest changes | `git pull` |
| View remote repository | `git remote -v` |
| List branches | `git branch` |
| Create a branch | `git switch -c feature-name` |
| Switch branches | `git switch branch-name` |

## 12.1 Recommended Git workflow

| Order | Action | Command |
|:---:|:---|:---|
| 1 | Check current branch | `git branch --show-current` |
| 2 | Check changes | `git status` |
| 3 | Review changes | `git diff` |
| 4 | Stage changes | `git add .` |
| 5 | Review staged changes | `git diff --cached` |
| 6 | Commit | `git commit -m "Meaningful message"` |
| 7 | Push | `git push` |
| 8 | Verify | `git status` |

---

# 13. Recommended `.gitignore`

Never upload Conda environments, Python cache files, Jupyter checkpoints or private credentials to GitHub.

Recommended `.gitignore`:

```gitignore
# Python cache
__pycache__/
*.py[cod]
*$py.class

# Virtual environments
venv/
.venv/
env/
.conda/

# Jupyter
.ipynb_checkpoints/

# Environment and secrets
.env
.env.*
!.env.example

# IDE
.vscode/
.idea/

# Operating system
.DS_Store
Thumbs.db
desktop.ini

# Logs
*.log

# Temporary files
*.tmp
*.bak

# Generated reports
*.pdf
*.xlsx

# Local datasets - review before committing
data/raw/*
data/interim/*
```

**Important:** If you want to version selected datasets, add explicit exceptions to `.gitignore`. Do not automatically ignore all project data if those files are intentionally part of your public repository.

---

# 14. Useful Verification Commands

## 14.1 Conda verification

| Check | Command |
|:---|:---|
| Conda version | `conda --version` |
| Conda information | `conda info` |
| Environment list | `conda env list` |
| Active environment | `conda info --envs` |
| Installed packages | `conda list` |

## 14.2 Python verification

| Check | Command |
|:---|:---|
| Python version | `python --version` |
| Python executable | `python -c "import sys; print(sys.executable)"` |
| Python search path | `python -c "import sys; print(sys.path)"` |
| Pip version | `python -m pip --version` |
| Installed packages | `python -m pip list` |

## 14.3 Jupyter verification

| Check | Command |
|:---|:---|
| Jupyter version | `jupyter --version` |
| Registered kernels | `jupyter kernelspec list` |
| Notebook version | `jupyter notebook --version` |
| IPython version | `ipython --version` |

## 14.4 Git verification

| Check | Command |
|:---|:---|
| Git version | `git --version` |
| Current branch | `git branch --show-current` |
| Remote repository | `git remote -v` |
| Working tree | `git status` |
| Recent commits | `git log --oneline -5` |

---

# 15. Final System Verification Checklist

Use this checklist whenever you configure a new terminal, update Anaconda or recover from a configuration problem.

| Component | Verification | Expected result | Status |
|:---|:---|:---|:---:|
| Anaconda | `conda --version` | Conda version displayed | [ ] |
| Anaconda Prompt | `conda activate uk-housing-env` | Environment activated | [ ] |
| PowerShell | `conda activate uk-housing-env` | Environment activated | [ ] |
| Command Prompt | `conda activate uk-housing-env` | Environment activated | [ ] |
| Git Bash | `conda activate uk-housing-env` | Environment activated | [ ] |
| Python | `python --version` | Python 3.12.16 | [ ] |
| Python executable | `sys.executable` | `envs/uk-housing-env/python.exe` | [ ] |
| VS Code | Select Python Interpreter | `uk-housing-env` | [ ] |
| Jupyter | Select Kernel | `Python (uk-housing-env)` | [ ] |
| Git | `git status` | Working tree status displayed | [ ] |
| GitHub | `git push` | Changes pushed successfully | [ ] |

---

# 16. Official Documentation and References

| Resource | Official link | Purpose |
|:---|:---|:---|
| Anaconda | [anaconda.com](https://www.anaconda.com/) | Anaconda installation and information |
| Conda documentation | [docs.conda.io](https://docs.conda.io/) | Conda configuration |
| Conda environments | [Managing environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) | Create and manage environments |
| Conda commands | [Command reference](https://docs.conda.io/projects/conda/en/latest/commands/index.html) | Command documentation |
| VS Code | [code.visualstudio.com](https://code.visualstudio.com/) | Editor documentation |
| VS Code Python | [Python environments](https://code.visualstudio.com/docs/python/environments) | Python interpreter configuration |
| VS Code Jupyter | [Jupyter notebooks](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) | Notebook configuration |
| Git | [git-scm.com](https://git-scm.com/) | Git documentation |
| Git for Windows | [gitforwindows.org](https://gitforwindows.org/) | Git Bash installation and updates |
| GitHub | [docs.github.com](https://docs.github.com/) | GitHub and repository documentation |

---

# 17. Important Rules to Remember

| Rule | Explanation |
|:---:|:---|
| 1 | Always activate `uk-housing-env` before working on this project. |
| 2 | Do not install project packages into the `base` environment. |
| 3 | Use the same Conda environment in PowerShell, CMD and Git Bash. |
| 4 | Ensure VS Code selects the correct Python interpreter. |
| 5 | Ensure Jupyter uses `Python (uk-housing-env)`. |
| 6 | Do not recreate an environment that already exists. |
| 7 | Do not reinstall Anaconda to fix a simple shell configuration issue. |
| 8 | Back up configuration files before modifying them. |
| 9 | Keep `environment.yml` updated when project dependencies change. |
| 10 | Never commit passwords, API keys, private credentials or sensitive datasets. |
| 11 | Restart the affected terminal after changing its startup configuration. |
| 12 | Verify the actual Python executable rather than relying only on the terminal prompt. |

---

# 18. Quick Reference — My Daily Commands

This is the section to use most frequently.

### Start project

```bash
conda activate uk-housing-env
cd ~/Desktop/PROJECTS/uk-housing-data-pipeline
code .
```

### Verify Python

```bash
python --version
python -c "import sys; print(sys.executable)"
```

### Start Jupyter

```bash
jupyter notebook
```

### Install a package

```bash
conda install package-name -y
```

### Check Git

```bash
git status
```

### Push changes to GitHub

```bash
git add .
git commit -m "Update project"
git push
```

### Deactivate Conda

```bash
conda deactivate
```

---

**Final reminder**

Your primary project configuration is:

| Setting | Value |
|:---|:---|
| Project | `uk-housing-data-pipeline` |
| Conda environment | `uk-housing-env` |
| Python | `3.12.16` |
| Anaconda | `C:\Users\imksa\anaconda3` |
| Project location | `C:\Users\imksa\Desktop\PROJECTS\uk-housing-data-pipeline` |
| VS Code interpreter | `uk-housing-env` |
| Jupyter kernel | `Python (uk-housing-env)` |

**The most important principle:** Activate the same Conda environment in whichever terminal you use, and ensure that VS Code and Jupyter point to that same environment. This keeps your entire development workflow consistent.

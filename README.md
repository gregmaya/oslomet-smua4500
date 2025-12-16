# OsloMet - SMUA4500 - SMART CITIES

This repository contains the notebooks and data used in the **SMART CITIES 4500** lessons. Each lesson’s notebook is designed to be reproducible in two ways:

- in the browser using **Google Colab** (easier, no installation) - requires Google account.,  
- on your own machine using **Python** and a local clone of the `student-notebooks` branch (more technical, but more flexible).


## Option A – Run in Google Colab (easiest)

1. At the top each reproducible notebook in this repo, there is an **“Open in Colab”** badge ![image](https://colab.research.google.com/assets/colab-badge.svg).
2. Open each lesson notebook by clicking the badge, which will launch it in Google Colab in your browser. (You need a Google account for this.)
3. If the notebook requires local data files:  
   - In Colab, use the folder icon on the left → “Upload” to upload the files from the [Datasets](data/index.qmd) section in this repo.
   - Alternatively, you can mount Google Drive (as described in the notebook) and put the files there.

> **⚠️ Note:** Colab gives you a fresh environment every time, so you may need to re‑upload data files or re‑run setup cells at the start of each new session.

***

## Option B – Run locally (recommended for deeper work)

This option assumes you want to clone the `student-notebooks` branch and run notebooks locally in an IDE such as VS Code. We reccomend **uv** to manage the virtual environment and dependencies.

> **⚠️ Note:** The **`student-notebooks`** branch contains the latest version of the student notebooks and corresponding `data/` folders for each lesson.


### **`student-notebooks`** structure

Once you've cloned the `student-notebooks` branch, the folder structure should look like this:

```text
.
├── src/
│   ├── week1.ipynb
│   ├── week2.ipynb
│   └── ...
├── data/
│   ├── demography/
│   │   ├── oslo_population.shp
│   │   ├── oslo_population.dbf
│   │   ├── oslo_population.prj
│   │   └── oslo_population.shx
│   ├── traffic/
│   │   └── oslo_metro.gpckg
│   └── ...
├── requirements.txt
├── pyproject.toml
└── README.md
```

***


### What is a virtual environment?

A **virtual environment** is an isolated Python installation that keeps the packages for one project separate from everything else on your system.  
This avoids version conflicts and makes it easier to reproduce results: everyone installs the same package versions listed in `requirements.txt` / `pyproject.toml` using uv.

### 0. Install uv (once only!)

<details>
  <summary>Mac OS</summary>
  
  **Homebrew:**

  ```bash
  brew install uv
  ```

</details>

<details>
  <summary>Windows</summary>

**PowerShell:**
    
    ```
    powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```
</details>


After installation, verify:

```bash
uv --version
```

### 1. Clone the `student-notebooks` branch

Choose a folder on your machine and clone only the student branch:

```bash
git clone --single-branch --branch student-notebooks https://github.com/gregmaya/oslomet-smua4500
```

When new lessons are published, you can pull updates with:

```bash
git pull
```

from inside the cloned folder.

### 2. Create and sync the environment with uv

From the project root:

```bash
# Create / update the virtual environment and install packages
uv sync
```

- `uv sync` reads the project configuration (e.g. `pyproject.toml` / `requirements.txt`), creates a `.venv/` directory, and installs the specified package versions.
- To upgrade packages (if the instructor announces an update):  

  ```bash
  uv sync --upgrade
  ```


### 3. Activate the virtual environment

Commonly, VSCode will auto-detect and use the `.venv` environment once it exists. If not, you can select it manually via the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`) → “Python: Select Interpreter” → choose the one in `.venv`.

If that doesn’t work, or if you want to run from the command line, you can activate the environment manually.

- **macOS / Linux (bash/zsh):**

  ```bash
  source .venv/bin/activate
  ```

- **Windows (PowerShell):**

  ```powershell
  .venv\Scripts\Activate.ps1
  ```

Your shell prompt should change, indicating the environment is active. To deactivate later, run:

```bash
deactivate
```

### 4. Run Jupyter / VS Code

**In VS Code:**

  1. Open the cloned folder in VS Code.  
  2. Install the Python and Jupyter extensions if prompted.  
  3. In any `.ipynb` notebook, use the “Select Kernel” dropdown and point it to the Python interpreter in `.venv` (VS Code usually auto‑detects it).  

Now you can open `src/weekXX/notebook.ipynb` and run the cells locally.

***

### 5. Keeping your local copy up to date

The instructor will periodically push new or updated notebooks and data to the `student-notebooks` branch. To update:

```bash
git pull
uv sync
```

- `git pull` fetches any new lesson folders and notebook changes.  
- `uv sync` ensures your virtual environment matches any updated dependencies.

***
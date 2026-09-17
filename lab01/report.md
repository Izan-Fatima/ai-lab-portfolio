# Lab 01 — Environment Setup: Report

**Author:** Izan Fatima
**Repository:** https://github.com/Izan-Fatima/ai-lab-portfolio

---

## 1. Installation Evidence

- Anaconda installed successfully on Windows 11.
- Created a dedicated Conda environment named `ai-lab` (Python 3.11) containing pandas, numpy,
  matplotlib, scikit-learn, jupyter, and ipykernel.
- Registered `ai-lab` as a Jupyter kernel and confirmed the notebook runs inside it:

```
Python version   : 3.11.16
Interpreter path : C:\Users\DELL\.conda\envs\ai-lab\python.exe
Platform          : Windows-10-10.0.26200-SP0

Running in ai-lab: True
```

- Installed Git for Windows (v2.55.0) and configured identity:

```
user.name  = Izan Fatima
user.email = 70177415@student.uol.edu.pk
init.defaultbranch = main
```

---

## 2. Task 1.3 — The Three Standard Inspections (Titanic dataset)

Dataset loaded from:
`https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv`

**Shape:** 891 rows × 15 columns

### 2.1 Structure — `df.head()`
First five rows confirmed expected columns: `survived, pclass, sex, age, sibsp, parch, fare,
embarked, class, who, adult_male, deck, embark_town, alive, alone`.

### 2.2 Composition — `df.info()`
```
survived       891 non-null   int64
pclass         891 non-null   int64
sex            891 non-null   str
age            714 non-null   float64
sibsp          891 non-null   int64
parch          891 non-null   int64
fare           891 non-null   float64
embarked       889 non-null   str
class          891 non-null   str
who            891 non-null   str
adult_male     891 non-null   bool
deck           203 non-null   str
embark_town    889 non-null   str
alive          891 non-null   str
alone          891 non-null   bool
```

### 2.3 Distribution — `df.describe()`
```
        survived   pclass       age    sibsp    parch      fare
count   891.0000  891.0000  714.0000  891.000  891.000  891.0000
mean      0.3838    2.3086   29.6991    0.523    0.382   32.2042
std       0.4866    0.8361   14.5265    1.103    0.806   49.6934
min       0.0000    1.0000    0.4200    0.000    0.000    0.0000
25%       0.0000    2.0000   20.1250    0.000    0.000    7.9104
50%       0.0000    3.0000   28.0000    0.000    0.000   14.4542
75%       1.0000    3.0000   38.0000    1.000    0.000   31.0000
max       1.0000    3.0000   80.0000    8.000    6.000  512.3292
```

### 2.4 Missing values, stated explicitly
| Column | Missing | % of rows |
|---|---|---|
| deck | 688 | 77.2% |
| age | 177 | 19.9% |
| embarked | 2 | 0.2% |
| embark_town | 2 | 0.2% |

---

## 3. In-Lab Exercises

**Exercise 2 — Missing columns (from `info()` alone):**
```python
missing_columns = {
    "deck": 688,
    "age": 177,
    "embarked": 2,
}
```

**Exercise 3 — Coefficient of variation (std / mean, largest first):**
```
parch       2.112
sibsp       2.108
fare        1.543
survived    1.268
age         0.489
pclass      0.362
```
**Largest: `parch`**

*Two-sentence answer:* `parch` has the highest coefficient of variation (2.11), meaning its
spread is more than twice its own mean — most passengers have 0 but a few have several, creating
a long tail. A model without feature scaling would treat `parch`'s variance as artificially more
important than an evenly-distributed column like `age`, purely because of scale.

**Exercise 4 — Git graph after three commits on `lab01/exercises`, merged into `main`:**
```
* 2934687 (HEAD -> main, origin/main, lab01/exercises) Update notes with exercise completion
* 0b4698  Add notes file for lab01
* e1701de Update README with Lab 01 section
* 57e2880 (lab01/inspection) Add project README
* 6079ecc Add lab01: environment setup notebook and exports
```

---

## 4. Home Assignment — `inspect.py`

`lab01/inspect.py` implements a single function, `inspect(path_or_url)`, that loads any CSV and
prints a compact standard report: shape, dtypes, per-column missing counts/percentages, and the
numeric summary (`df.describe()`).

Run against three public datasets:

| Dataset | Source | Shape | Missing values |
|---|---|---|---|
| Titanic | seaborn-data (GitHub) | 891 × 15 | deck, age, embarked, embark_town |
| Iris | seaborn-data (GitHub) | 150 × 5 | None |
| Tips | seaborn-data (GitHub) | 244 × 7 | None |

Full output for each run is saved alongside the script:
`lab01/report_titanic.txt`, `lab01/report_iris.txt`, `lab01/report_tips.txt`.

Committed on branch `lab01/homework`, merged into `main`.

---

## 5. Deliverables Summary

| File | Status |
|---|---|
| `lab01/Lab1_setup.ipynb` | Executed, all outputs visible |
| `lab01/Lab1_setup.html`, `lab01/Lab1_setup.pdf` | Exported |
| `lab01/inspect.py` | Complete, tested on 3 datasets |
| `requirements.txt` | Generated via `pip freeze` from `ai-lab` |
| `.gitignore` | Excludes `.ipynb_checkpoints/`, `__pycache__/` |
| `lab01/report.md` | This file |

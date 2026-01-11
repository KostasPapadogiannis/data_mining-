# Οδηγίες Εγκατάστασης και Εκτέλεσης

Αυτό το αρχείο περιέχει **αναλυτικές οδηγίες** για το πώς να στήσεις το project στο δικό σου υπολογιστή.

---

## 📋 Προαπαιτούμενα

- **Python 3.12** ή νεότερο
- **Git** εγκατεστημένο
- Περίπου **500 MB ελεύθερου χώρου** (για το dataset + dependencies)

---

## 🚀 Βήμα 1: Clone το Repository

Άνοιξε ένα terminal και γράψε:

```bash
git clone https://github.com/KostasPapadogiannis/data_mining.git
cd data_mining
```

---

## 📦 Βήμα 2: Δημιουργία Virtual Environment

Για να απομονώσεις τις βιβλιοθήκες του project:

```bash
# Δημιουργία του virtual environment
python3 -m venv venv

# Ενεργοποίηση (Linux/Mac)
source venv/bin/activate

# Ενεργοποίηση (Windows)
venv\Scripts\activate
```

Όταν το venv είναι ενεργοποιημένο, θα δεις `(venv)` στην αρχή της γραμμής του terminal.

---

## 📚 Βήμα 3: Εγκατάσταση Dependencies

Εγκατέστησε όλες τις απαραίτητες βιβλιοθήκες:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

**Σημείωση:** Η εγκατάσταση του TensorFlow (για το LSTM) μπορεί να πάρει 5-10 λεπτά.

---

## 📥 Βήμα 4: Κατέβασμα του Raw Dataset

Το αρχικό dataset (`household_power_consumption.txt`) είναι **πολύ μεγάλο (~120 MB)** και δεν ανεβαίνει στο GitHub.

### Επιλογή 1: Κατέβασμα από UCI Repository (Συνιστάται)

1. Πήγαινε στο: https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption
2. Κατέβασε το αρχείο **`household_power_consumption.zip`**
3. Αποσυμπίεσέ το
4. Μετακίνησε το αρχείο `household_power_consumption.txt` στο φάκελο `data/`:

```bash
# Από το directory όπου κατέβηκε το αρχείο
mv household_power_consumption.txt /path/to/data_mining/data/
```

### Επιλογή 2: Χρήση του καθαρού dataset (Γρήγορη λύση)

Αν **ΔΕΝ** θέλεις να τρέξεις το notebook προεπεξεργασίας, μπορείς να χρησιμοποιήσεις μόνο το καθαρό dataset που ήδη υπάρχει:

- Το αρχείο `data/df_daily_clean.csv` **ήδη υπάρχει** στο repository
- Μπορείς να προσπεράσεις το `data_preprocessing.ipynb` και να τρέξεις απευθείας το `modeling.ipynb`

---

## 🔍 Βήμα 5: Επαλήθευση

Έλεγξε ότι όλα είναι στη θέση τους:

```bash
# Έλεγχος δομής φακέλων
ls -la data/
# Πρέπει να δεις: df_daily_clean.csv
# Και (προαιρετικά): household_power_consumption.txt

ls -la notebooks/
# Πρέπει να δεις: data_preprocessing.ipynb, modeling.ipynb

ls -la results/
# Πρέπει να δεις: διάφορα .png και .csv αρχεία
```

---

## 🎯 Βήμα 6: Εκτέλεση των Notebooks

### Άνοιγμα Jupyter Notebook

```bash
# Βεβαιώσου ότι το venv είναι ενεργοποιημένο
jupyter notebook
```

Θα ανοίξει ένα browser tab. Πλοήγησε στον φάκελο `notebooks/` και:

### A) Notebook Προεπεξεργασίας (Προαιρετικό)

Αν κατέβασες το raw dataset:

1. Άνοιξε `data_preprocessing.ipynb`
2. Τρέξε όλα τα κελιά με: **Kernel → Restart & Run All**
3. Αυτό θα δημιουργήσει το `data/df_daily_clean.csv`

### B) Notebook Μοντελοποίησης (Κύριο)

1. Άνοιξε `modeling.ipynb`
2. Τρέξε όλα τα κελιά με: **Kernel → Restart & Run All**
3. Αυτό θα:
   - Εκπαιδεύσει όλα τα μοντέλα (Classification, Regression, Clustering, Association Rules, Time Series)
   - Δημιουργήσει όλα τα plots στο `results/`

**Σημείωση:** Η εκτέλεση του `modeling.ipynb` μπορεί να πάρει 10-20 λεπτά (ιδίως το LSTM training).

---

## 📊 Βήμα 7: Αποτελέσματα

Μετά την εκτέλεση των notebooks:

- **Plots**: Όλα τα διαγράμματα θα είναι στο `results/`
- **Αναφορά**: Διάβασε το `report/report.md` για πλήρη ανάλυση

---

## 🐛 Αντιμετώπιση Προβλημάτων

### Πρόβλημα: "ModuleNotFoundError: No module named 'X'"

**Λύση:**
```bash
pip install X
# Ή
pip install -r requirements.txt --force-reinstall
```

### Πρόβλημα: "FileNotFoundError: data/household_power_consumption.txt"

**Λύση:** Κατέβασε το raw dataset (βλέπε Βήμα 4) ή χρησιμοποίησε μόνο το `modeling.ipynb` (που χρησιμοποιεί το `df_daily_clean.csv`).

### Πρόβλημα: Jupyter Notebook δεν εκκινεί

**Λύση:**
```bash
pip install --upgrade jupyter
jupyter notebook
```

### Πρόβλημα: TensorFlow errors με CUDA

**Λύση:** Το TensorFlow θα τρέξει στο CPU (όχι GPU). Αυτό είναι OK, απλά θα είναι λίγο πιο αργό. Αγνόησε τα CUDA warnings.

---


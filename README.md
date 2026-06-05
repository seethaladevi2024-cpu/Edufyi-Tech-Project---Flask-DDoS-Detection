# DDoS Detection System — ML Flask Web App

A professional Machine Learning–powered web application that classifies network traffic as **DDoS** or **BENIGN** using a Random Forest model.

---

## 📁 Folder Structure

```
project/
│
├── app.py                        ← Flask backend
├── model.pkl                     ← Trained Random Forest model
├── ddos_predictions.csv          ← Auto-generated after prediction
├── benign_predictions.csv        ← Auto-generated after prediction
├── COLAB_SETUP.py                ← Step-by-step Google Colab guide
│
├── uploads/                      ← Uploaded CSV files (auto-created)
│
├── static/
│   ├── style.css
│   ├── prediction_pie_chart.png  ← Auto-generated after prediction
│   └── prediction_bar_chart.png  ← Auto-generated after prediction
│
└── templates/
    ├── index.html
    └── result.html
```

---

## 🚀 Local Setup

```bash
# 1. Install dependencies
pip install flask scikit-learn pandas numpy matplotlib werkzeug

# 2. Place your trained model
cp /path/to/your/model.pkl ./model.pkl

# 3. Run the app
python app.py

# 4. Open in browser
#    http://localhost:5000
```

---

## ☁️ Google Colab Setup

Follow the steps in **COLAB_SETUP.py**:

1. Install packages: `flask pyngrok scikit-learn pandas numpy matplotlib`
2. Create folder structure
3. Write all files using `%%writefile` magic
4. Save your model as `model.pkl`
5. Launch Flask + ngrok tunnel
6. Click the public ngrok URL to open the app

---

## 📊 Features

| Feature | Details |
|---------|---------|
| **Upload** | Drag & drop or browse CSV files (up to 50 MB) |
| **Model** | Random Forest (sklearn) via `model.pkl` |
| **Preprocessing** | Auto-drops Label/non-numeric cols, fills NaN with median |
| **Predictions** | Classifies each row as `DDoS` or `BENIGN` |
| **Accuracy** | Computed if CSV contains a `Label` column |
| **Report** | Full sklearn `classification_report` |
| **Charts** | Pie chart + Bar chart saved as PNG |
| **Downloads** | Filtered CSVs: `ddos_predictions.csv`, `benign_predictions.csv` |

---

## 📄 CSV Format

Your CSV should contain **numeric feature columns**. A `Label` column is optional but enables accuracy scoring:

```
Flow Duration, Total Fwd Packets, Total Bwd Packets, ..., Label
```

Compatible with **CIC-IDS-2017** and **CIC-DDoS-2019** datasets.

---

## 🔧 Replacing the Model

The app loads `model.pkl` at prediction time. To use your own model:

```python
import pickle
from sklearn.ensemble import RandomForestClassifier

# Train your model
clf = RandomForestClassifier(...)
clf.fit(X_train, y_train)

# Save it
with open('model.pkl', 'wb') as f:
    pickle.dump(clf, f)
```

Ensure your model outputs labels `'DDoS'` or `'BENIGN'` (or `1` / `0` — the app maps integers automatically).

---

## 🎨 Tech Stack

- **Backend**: Python 3, Flask
- **ML**: scikit-learn (Random Forest)
- **Data**: pandas, numpy
- **Charts**: matplotlib
- **Frontend**: HTML5, Bootstrap 5, custom CSS
- **Fonts**: Syne (headings), DM Sans (body)
- **Tunnel**: pyngrok (for Colab)

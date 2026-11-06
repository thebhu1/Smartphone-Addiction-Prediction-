# 📱 Smartphone Addiction Prediction System (v1.0.0)

> A modern, full-stack Machine Learning web application and REST API that evaluates daily smartphone usage behaviors, predicts addiction risk levels, and generates personalized clinical-grade PDF wellness reports.

![Python](https://img.shields.io/badge/Language-Python_3.10%2B-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Framework-Flask_3.x-000000?logo=flask&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/ML-Scikit--Learn-F7931E?logo=scikit-learn&logoColor=white)
![JavaScript](https://img.shields.io/badge/Frontend-Vanilla_JS-F7DF1E?logo=javascript&logoColor=black)
![CSS3](https://img.shields.io/badge/Design-Responsive_CSS3-1572B6?logo=css3&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 📖 Table of Contents

- [About the Project](#about-the-project)
- [The Problem It Solves](#the-problem-it-solves)
- [Key Features](#key-features)
- [Behavioral Metrics Analyzed](#behavioral-metrics-analyzed)
- [Machine Learning Performance](#machine-learning-performance)
- [Project Architecture & File Structure](#project-architecture--file-structure)
- [How It Works (Technical Overview)](#how-it-works-technical-overview)
- [REST API Endpoints](#rest-api-endpoints)
- [How to Install & Run Locally](#how-to-install--run-locally)
- [Testing the Application](#testing-the-application)
- [License](#license)

---

## 💡 About the Project

**Smartphone Addiction Prediction System (SAPS)** bridges the gap between machine learning research and everyday digital wellness.

Instead of guessing whether your phone habits are healthy, you enter key usage indicators—such as daily screen time, social media consumption, night usage, unlock frequency, and sleep disturbance. The system uses a trained Machine Learning model to evaluate your habits, classifies your dependency risk into **Low**, **Moderate**, or **High**, and dynamically compiles an official wellness report ready for immediate download.

---

## 🛑 The Problem It Solves

* **Subjective Guesswork:** Most people underestimate their phone habits and don't recognize unhealthy patterns until sleep or productivity suffers.
* **Disconnected Screen Time Tools:** Built-in phone dashboards show raw screen minutes, but fail to correlate usage with critical risk factors like late-night screen exposure or sleep disruption.
* **Complex Data Science Silos:** Advanced predictive algorithms often remain buried inside Jupyter Notebooks rather than being accessible to everyday users.

**SAPS** solves all three by packaging a trained Random Forest classification model inside an intuitive, responsive web application backed by an asynchronous REST API and an in-memory PDF reporting engine.

---

## ✨ Key Features

- ⚡ **Real-Time ML Inference:** Instantly predicts addiction risk (**Low**, **Moderate**, or **High**) with class probability distributions powered by an optimized Random Forest classifier.
- 🔄 **Interactive Hours $\leftrightarrow$ Minutes Toggle:** Dynamic client-side unit switch that instantly converts input values and readjusts validation boundaries without resetting the form.
- 📈 **Weighted Digital Load (WDL):** Computes a specialized composite index (0–10 scale) combining screen volume, social media density, gaming duration, and night usage.
- 🛡️ **Non-Linear Edge Risk Overrides:** Intelligent heuristic safeguards that flag extreme behaviors (e.g., night usage > 4 hrs paired with sleep disturbance > 8/10) even when overall daily hours appear moderate.
- 📄 **In-Memory PDF Report Generation:** Dynamic clinical-style report generation using **ReportLab** and Python's `io.BytesIO` stream—creating downloadable A4 PDFs on the fly without writing temporary files to server disk.
- 📊 **Model Analytics Dashboard:** Dedicated visual benchmarking portal displaying confusion matrices, accuracy comparisons (Random Forest vs. SVM vs. Logistic Regression), and feature importance plots.
- 🌐 **Decoupled RESTful API:** Standardized JSON endpoints allowing seamless integration with future Android/iOS mobile clients or external health platforms.
- 🚀 **Zero External Database Overhead:** Completely stateless, privacy-friendly design utilizing serialized `.pkl` models with no persistent personal data logging.

---

## 📊 Behavioral Metrics Analyzed

The system analyzes 10 quantitative parameters to assess digital dependency:

| Metric | Description | Acceptable Range | Unit |
| :--- | :--- | :---: | :---: |
| **Daily Screen Time** | Total active display duration per day | 1.0 – 16.0 | Hours |
| **Social Media Time** | Duration on social platforms (Instagram, TikTok, etc.) | 0.0 – 8.0 | Hours |
| **Gaming Time** | Time spent playing mobile games | 0.0 – 6.0 | Hours |
| **Daily Notifications** | Total incoming alerts and notification pings | 10 – 1000 | Alerts / Day |
| **App Launches** | Total instances applications are opened daily | 20 – 500 | Launches / Day |
| **Night Usage** | Phone usage between 11:00 PM and 6:00 AM | 0.0 – 5.0 | Hours |
| **Sleep Disturbance** | Self-assessed sleep impact score | 0 – 10 | Rating Scale |
| **Phone Unlocks** | Number of times the device is unlocked per day | 20 – 500 | Unlocks / Day |
| **Weekend Usage Increase** | Percentage increase in weekend usage vs. weekdays | -20% – +100% | Percent (%) |
| **Average Session Duration** | Mean duration per single continuous phone session | 2 – 30 | Minutes |

---

## 🧠 Machine Learning Performance

Three classification models were trained and benchmarked using stratified 80/20 train-test splits and Macro-averaging:

| Model | Accuracy | Precision | Recall | F1-Score | Status |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Random Forest** | **92.5%** | **0.926** | **0.925** | **0.925** | 🏆 **Production Model** |
| **Support Vector Machine (SVM)** | 91.0% | 0.908 | 0.910 | 0.909 | Evaluated Alternative |
| **Logistic Regression** | 89.5% | 0.893 | 0.895 | 0.894 | Baseline Benchmark |

### Top Predictive Features (Random Forest)
1. **Sleep Disturbance** (12.9%)
2. **Daily Screen Time** (11.5%)
3. **Daily Notifications** (11.5%)
4. **Average Session Duration** (10.5%)
5. **Social Media Time** (10.5%)

---

## 📁 Project Architecture & File Structure

```text
smartphone-addiction-prediction/
│
├── app.py                      # Flask server, route controller, session & PDF streaming
├── diagnostic.py               # Model health check and environment validation script
├── generate_dataset.py         # Synthetic behavioral dataset generator
├── train_model.py              # ML pipeline: training, benchmarking & serialization
├── requirements.txt            # Python dependencies manifest
├── README.md                   # Project documentation
│
├── data/
│   ├── raw/                    # Raw usage datasets (CSV format)
│   └── processed/              # Cleaned, standardized training data
│
├── models/
│   ├── addiction_model.pkl     # Production Random Forest classifier
│   ├── scaler.pkl              # Fitted StandardScaler for numerical features
│   ├── model_metrics.json      # Offline evaluation metrics cache
│   └── *.png                   # Visual confusion matrices & feature importance charts
│
├── notebooks/
│   └── exploratory_analysis.ipynb # Jupyter notebook for EDA and statistical plots
│
├── src/
│   ├── __init__.py             # Python package marker
│   ├── data_preprocessing.py   # Outlier handling, encoding, and scaling pipelines
│   ├── model_training.py       # ModelTrainer class (RF, SVM, LR training harness)
│   └── prediction.py           # AddictionPredictor class (inference, heuristics, WDL)
│
├── static/
│   ├── css/style.css           # Custom styles, responsive grid, and risk badge colors
│   └── js/
│       ├── performance.js      # Analytics dashboard charts and metric renderers
│       └── script.js           # Form events, hours/minutes toggle & async API calls
│
├── templates/
│   ├── index.html              # Modern landing page
│   ├── predict.html            # 10-input assessment form & dynamic result view
│   └── model_performance.html  # Model benchmarking and visualization dashboard
│
└── tests/
    └── test_prediction.py      # Automated unit tests using pytest
```

---

## ⚙️ How It Works (Technical Overview)

1. **Client Input & Normalization:** The user completes the 10-parameter form in `predict.html`. If the minutes toggle is active, `script.js` converts minute values into hours and validates boundaries.
2. **Asynchronous Request Dispatch:** `handleFormSubmit()` intercepts the submit event, serializes inputs to JSON, and dispatches a `POST` request to `/api/predict` via the `fetch()` API.
3. **Server Validation & Preprocessing:** In `app.py`, Flask parses the JSON payload. `AddictionPredictor.validate_input()` checks numeric data types and range bounds.
4. **Standardization & Inference:** The input dictionary is converted into a Pandas DataFrame, scaled via the pre-loaded `StandardScaler`, and evaluated by the `Random Forest` model to produce class probabilities.
5. **Heuristic Evaluation & WDL:** The predictor computes the **Weighted Digital Load (WDL)**, checks for non-linear risk overrides (e.g., severe sleep disruption), and builds customized behavioral advice.
6. **Dynamic DOM Rendering:** The frontend receives the JSON response, dynamically displays the risk badge (green/orange/red), plots probability bars, and enables the **"Download Report (PDF)"** button.
7. **In-Memory PDF Generation:** When clicked, `/generate-report` invokes ReportLab to format a multi-page document into an in-memory `io.BytesIO` binary stream, streamed directly to the browser as an attachment.

---

## 🔌 REST API Endpoints

| Method | Endpoint | Description | Payload / Response |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/predict` | Computes addiction risk and probabilities | **Body:** 10 usage features<br>**Return:** Prediction JSON & recommendations |
| `POST` | `/generate-report` | Builds and streams personalized wellness PDF | **Body:** Usage & result payload<br>**Return:** Binary PDF (`application/pdf`) |
| `GET` | `/api/health` | Health check verifying model status | **Return:** `{"status": "healthy", ...}` |
| `GET` | `/api/feature_info` | Provides range boundaries and units for features | **Return:** Feature metadata dictionary |
| `GET` | `/api/model_metrics` | Returns accuracy, precision, and F1 benchmarks | **Return:** Comparative model metrics JSON |

---

## 🚀 How to Install & Run Locally

### Prerequisites
* **Python 3.10+** installed on your system ([Download Python](https://www.python.org/))
* **Git** installed ([Download Git](https://git-scm.com/))

### Installation Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/smartphone-addiction-prediction.git
   cd smartphone-addiction-prediction
   ```

2. **Create and activate a virtual environment:**
   * **Windows (PowerShell):**
     ```powershell
     python -m venv venv
     .\venv\Scripts\Activate.ps1
     ```
     *(If script execution is disabled: `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`)*
   * **macOS / Linux:**
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```

3. **Install required dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Verify environment and model files:**
   ```bash
   python diagnostic.py
   ```

5. **Start the Flask server:**
   ```bash
   python app.py
   ```

6. **Open in your web browser:**
   Navigate to 👉 **`http://localhost:5000`**

---

## 🧪 Testing the Application

The repository includes automated unit tests to verify probability distributions, boundary heuristics, and index calculations:

1. **Run unit tests with Pytest:**
   ```bash
   pytest -v
   ```

2. **Run targeted logic tests:**
   ```bash
   python test_prompt1_logic.py
   python test_specific_input.py
   ```

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).


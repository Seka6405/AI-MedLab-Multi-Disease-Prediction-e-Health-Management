# AI Med Lab — AI-Powered Disease Prediction & Patient Management

AI Med Lab is an educational healthcare application that combines machine-learning-based symptom analysis with patient-history management and role-based workflows for patients, doctors, and nurses. It is the updated version of the **Healthcare Disease Prediction and Patient Management System** project.

> **Disclaimer:** AI Med Lab is a demonstration/educational project, not a medical device. Predictions and health information are not a diagnosis or treatment recommendation. Users should consult a qualified healthcare professional for medical decisions.

## Overview

The application lets users enter age, gender, and symptoms to receive a model-generated disease prediction with a confidence score. It also supports patient history, health guidance, doctor review, nurse reports, and downloadable PDF health reports.

## Key Features

- **Machine-learning prediction:** XGBoost classifier using age, gender, and symptom inputs.
- **Role-based workflows:** Separate patient, doctor, and nurse dashboard views.
- **Authentication:** Registration and login endpoints with password hashing described in the project architecture.
- **Patient history:** Save, view, and delete prediction-history records.
- **Doctor workflow:** View patient records and add health tips and appointment dates.
- **Nurse workflow:** View patient information and add nurse reports.
- **Health recommendations:** Retrieve disease-specific health tips and structured recommendations.
- **PDF reports:** Generate and download formatted reports containing patient information, prediction details, doctor guidance, and nurse notes.
- **REST API:** Flask backend connects the browser-based frontend to prediction and patient-management functionality.

## Technology Stack

| Area | Technologies |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Frontend server | Python `http.server` |
| Backend | Python, Flask, Flask-CORS |
| Machine learning | XGBoost, scikit-learn |
| Data processing | pandas, NumPy |
| Model serialization | joblib / pickle model artifacts |
| Reports | ReportLab |
| Data storage | JSON files and CSV dataset |
| Local session handling | Browser `localStorage` |

## Machine Learning

The documented model is an **XGBoost multi-class classifier**.

- **Inputs:** 22 features — age, gender, and symptom indicators.
- **Outputs:** 11 disease classes, as listed in the model reference.
- **Reported metrics in the project documentation:**
  - Training accuracy: 95.2%
  - Test accuracy: 93.8%
  - Cross-validation score: 94.1%

These figures are from the project's architecture documentation. They should be revalidated against the current model, dataset split, and evaluation procedure before being used as formal performance claims.

## Architecture

```text
Browser UI (HTML / CSS / JavaScript)
        |
        | HTTP requests
        |
        +--> Frontend server: localhost:8000
        |
        +--> Flask REST API: localhost:5000
                    |
                    +--> Authentication and role workflows
                    +--> XGBoost prediction + encoders
                    +--> Patient history and report data
                    +--> Health recommendations
                    +--> ReportLab PDF generation
```

### Main components

- `frontend/index.html` — login and registration interface
- `frontend/dashboard.html` — main role-based dashboard
- `frontend/script.js` — browser-side interactions and API calls
- `frontend/style.css` — UI styling
- `Backend/app.py` — Flask application entry point
- `Backend/routes/` — route modules, including authentication and prediction
- `Backend/model/` — model, encoders, training data, and related files

*The paths above follow the architecture reference; adjust the capitalization or folder names if your repository differs.*

## API Highlights

The architecture reference documents these routes:

| Method | Endpoint | Purpose |
|---|---|---|
| `POST` | `/register` | Register a user |
| `POST` | `/login` | Log in |
| `GET` | `/symptoms` | Get available symptoms |
| `POST` | `/predict` | Predict a disease from submitted inputs |
| `GET` | `/patient_history/<email>` | Retrieve a patient's history |
| `POST` | `/save_patient_history` | Save a history record |
| `POST` | `/add_health_tips` | Add health tips |
| `GET` | `/all_records` | Retrieve patient records for doctor workflow |
| `GET` | `/nurse/patients` | Retrieve patients for nurse workflow |
| `POST` | `/nurse/generate_report` | Add a nurse report |
| `GET` | `/doctor/patients` | Retrieve patients for doctor workflow |
| `POST` | `/doctor/add_health_tips` | Add doctor guidance and appointment date |
| `POST` | `/generate_pdf_report/<email>` | Generate/download a PDF report |
| `GET` | `/health_recommendations/<disease>` | Retrieve structured health recommendations |
| `DELETE` | `/patient_history/<email>/record` | Delete one history record |
| `DELETE` | `/patient_history/<email>/clear` | Clear a patient's history |

Confirm the actual routes and request formats against the code in your current repository before publishing or integrating the API.

## Getting Started

### Prerequisites

- Python 3.10+ (use the version supported by your project dependencies)
- pip
- A modern web browser

### 1. Clone the repository

Replace the placeholder URL with your actual GitHub repository URL:

```bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

If the repository includes a `requirements.txt` file:

```bash
pip install -r requirements.txt
```

Otherwise, install the dependencies specified by your project and create a `requirements.txt` so others can reproduce the environment. The documented stack includes Flask, Flask-CORS, XGBoost, scikit-learn, pandas, NumPy, ReportLab, and joblib.

### 4. Start the backend

From the backend directory, run the Flask application using the path and entry point in your repository. For the documented layout, this may be:

```bash
cd Backend
python app.py
```

The architecture reference specifies the API at `http://localhost:5000`.

### 5. Start the frontend

Open a second terminal and serve the frontend directory on port 8000. For example, if the folder is named `frontend`:

```bash
python -m http.server 8000 --directory frontend
```

Then open:

```text
http://localhost:8000
```

If your project uses different directory names or startup commands, update these steps to match the repository.

## Example Prediction Request

The documented prediction endpoint accepts age, a gender encoding, and a list of symptoms:

```http
POST http://localhost:5000/predict
Content-Type: application/json
```

```json
{
  "age": 35,
  "gender": 0,
  "symptoms": ["Fever", "Cough", "Fatigue"]
}
```

The documented response includes a predicted disease, confidence value, and timestamp. Actual values depend on the model and input.

## Security and Limitations

This project is intended as a learning and demonstration application. Before any real-world or production use:

- Replace JSON-file storage with a properly managed database and add concurrency-safe data access.
- Review authentication, password hashing, session management, authorization, and secret handling.
- Do not rely on client-side `localStorage` as the sole security control.
- Configure CORS and debug mode safely for the deployment environment.
- Add appropriate audit logging, monitoring, validation, backup, and access controls.
- Assess privacy, consent, and applicable healthcare/data-protection requirements before storing real patient information.
- Independently validate model quality, bias, calibration, and clinical suitability with qualified experts.

## Future Improvements

- Migrate file-based storage to a managed database.
- Introduce secure token-based authentication and stronger role-based authorization.
- Add automated tests for API routes and prediction workflows.
- Package the app for reproducible deployment.
- Improve model evaluation with documented splits, per-class metrics, and error analysis.

## Project Status

The documented architecture is version 2.0. Verify the current implementation, dependencies, route names, and model metrics against the latest code before treating this README as an exact deployment guide.

## Author

**Sekhar Kolluru**

- GitHub: [@Seka6405](https://github.com/Seka6405)
- Email: [sekharkolluru06@gmail.com](mailto:sekharkolluru06@gmail.com)

---

If you find the project useful, feel free to explore the repository and share feedback.

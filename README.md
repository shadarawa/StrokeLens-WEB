# StrokeLens-WEB
Graduation Project: AI-powered Stroke Risk Prediction Web Application
# StrokeLens Web Security Application

StrokeLens is a secure Flask based web application designed to support scenario based stroke risk prediction through a role aware clinical interface.

This repository focuses on the web application layer and the web security controls implemented around authentication, authorization, clinical data handling, prediction requests, secure reporting, and governed model retraining.

## Project Purpose

The project demonstrates how a machine learning based healthcare system can be integrated into a secure web application.

The web platform allows authorized users to submit clinical data, select an appropriate prediction scenario, review prediction results, generate verifiable reports, and access administrative model management functions according to their assigned roles.

The system is an academic prototype and is not intended to replace professional medical diagnosis or clinical judgment.

## Web Application Features

1. Secure user authentication

2. One time password verification by email

3. Role based access control

4. Clinician, data scientist, and administrator roles

5. Scenario based stroke risk prediction

6. Clinical input validation

7. Explainability and prediction review

8. Secure PDF report generation and verification

9. User profile and password management

10. Administrative audit log monitoring

11. Controlled model retraining workflows

12. Account lockout after repeated failed login attempts

## Web Security Features

### Password Security

User passwords are never stored as plain text. Passwords are hashed using Werkzeug password hashing functions before they are stored in the database.

The application also applies password complexity validation when a password is changed or reset.

### One Time Password Authentication

After successful username, password, and role validation, the system generates a six digit OTP.

The OTP is hashed before being stored in the session and has a limited validity period.

This provides an additional authentication layer and reduces the risk associated with stolen passwords.

### Role Based Access Control

The system defines separate permissions for clinicians, data scientists, and administrators.

Sensitive functions such as case review, report generation, report verification, and model retraining are restricted according to the authenticated user's role.

### Account Lockout

Repeated failed login attempts are recorded.

After five failed attempts, the account is temporarily locked to reduce brute force and password guessing attacks.

### Session Security

Authenticated sessions have a limited lifetime.

The application clears temporary authentication data after OTP verification and uses a secret key supplied through an environment variable.

Production deployment should additionally enable secure, HTTP only, and SameSite cookie settings.

### Audit Logging

Security relevant and operational activities are recorded to support accountability, traceability, and incident review.

Examples include login activity, clinical case actions, report generation, report verification, and model retraining operations.

### Cryptographic Report Verification

Generated reports can be digitally signed and verified using elliptic curve digital signatures.

The public key may be distributed for verification, while the private signing key must never be committed to the repository.

### Secret Management

Email credentials, application secret keys, database connection strings, and private cryptographic keys are excluded from source control.

These values must be provided through environment variables or an approved secret management service.

## Prediction Scenarios

The application supports three information availability scenarios.

### S1 Early Strict

Uses demographic information and medical history variables that are available before or during an initial early assessment.

### S2 Early Admission

Extends S1 with indicators that are available during admission.

### S3 In Hospital Update

Extends S2 with hospitalization derived variables.

The scenario separation prevents early predictions from using information that would only become available later. This reduces information leakage and makes the evaluation more realistic.

## Why Model Training Is Included

Model training is included because the web application is not only a static user interface.

The application communicates with trained machine learning models to produce stroke risk predictions.

The initial training process learns patterns from historical, approved clinical data. During inference, the web application loads the trained model and applies it to newly submitted patient information.

The project also includes governed retraining to demonstrate controlled model lifecycle management.

Retraining is not performed directly after every prediction. Only reviewed, approved, and labeled cases should be considered for future training.

This design is used for the following reasons:

1. To improve the model when reliable new data becomes available

2. To reduce the effect of model drift

3. To prevent unverified user input from automatically changing the deployed model

4. To preserve model versioning and traceability

5. To compare a newly trained challenger model with the currently deployed model before replacement

6. To maintain human and administrative control over model updates

The project provides two retraining approaches.

### Quick Retraining

Quick retraining updates one selected scenario using newly approved and labeled cases while preserving the active decision threshold.

### Full Retraining

Full retraining rebuilds and evaluates all supported candidate models and scenarios.

The best challenger is compared with the current deployed model before any replacement decision is made.

This controlled approach is safer than unrestricted online learning, particularly in a healthcare related application.

## Technologies

1. Python

2. Flask

3. HTML

4. CSS

5. JavaScript

6. SQLite or PostgreSQL

7. Werkzeug password hashing

8. Flask Mail

9. Scikit learn

10. XGBoost

11. SHAP

12. ReportLab

13. Cryptography

## Project Structure

```text
StrokeLens-Web-Security/
│
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
├── .env.example
│
├── templates/
│   ├── index.html
│   ├── reset_password.html
│   └── verify.html
│
├── static/
│   ├── logo.png
│   └── ecg-bg.jpg.jpg
│
├── app/
│   ├── core/
│   ├── services/
│   ├── database.py
│   └── models.py
│
├── ml/
│   ├── retrain.py
│   └── retrain_full_all_models.py
│
└── artifacts/
    └── keys/
        └── ecdsa_public.pem
```

## Local Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/StrokeLens-Web-Security.git
cd StrokeLens-Web-Security
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Activate it on Linux or macOS:

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Create the local environment file:

```bash
copy .env.example .env
```

On Linux or macOS:

```bash
cp .env.example .env
```

Set secure local values inside `.env`.

Run the application:

```bash
python app.py
```

Open the application at:

```text
http://127.0.0.1:5000
```

## Required Environment Variables

```env
STROKEWEB_SECRET_KEY=your-secure-random-secret
MAIL_USERNAME=your-email@example.com
MAIL_PASSWORD=your-email-app-password
DATABASE_URL=sqlite:///app_dev.db
```

Never commit the real `.env` file.

## Security Deployment Notes

Before production deployment:

1. Disable Flask debug mode

2. Use HTTPS

3. Use secure and HTTP only cookies

4. Configure CSRF protection

5. Use a production WSGI server

6. Replace SQLite with a managed database when appropriate

7. Store secrets in a secure secret manager

8. Rotate all exposed credentials

9. Use a persistent reset token store with expiration

10. Add request rate limiting

11. Restrict allowed file paths and uploaded file types

12. Perform dependency and source code security scanning

## Medical Disclaimer

StrokeLens is an academic prototype developed for educational and research purposes.

Its predictions must not be considered a medical diagnosis or used as the sole basis for clinical decisions.

All outputs should be reviewed by qualified healthcare professionals.

## Team

Developed as a graduation project at Mutah University, Faculty of Information Technology.

## License

This repository may be distributed under an academic or open source license selected by the project team.

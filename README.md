# StrokeLens-WEB
Graduation Project: AI-powered Stroke Risk Prediction Web Application
# StrokeLens Web Security

StrokeLens Web Security is a Flask based web application that demonstrates secure authentication and web security mechanisms.

This repository focuses only on the web application and web security components of StrokeLens.

The web application was developed using Flask for backend routing and HTML, CSS, and JavaScript for the user interface.

## Project Overview

The authentication process uses two stages.

First, the system verifies the username or email address, password, and selected user role.

Second, the system generates a six digit one time password and sends it to the user's registered email address.

The user must enter the correct OTP before accessing the protected pages of the application.

Passwords are stored as secure hashes using Werkzeug and are never stored as plain text.

The application also applies password complexity requirements when users update or reset their passwords.

To reduce brute force attacks, the system tracks failed login attempts and temporarily locks the account after five unsuccessful attempts.

Role based access control ensures that users can access only the pages and functions assigned to their roles.

The system also uses limited session lifetimes, environment variables for sensitive configuration, secure password reset functionality, and security alert emails.

This repository does not include machine learning training, prediction, result analysis, retraining, reports, or logs.

It focuses only on the implementation of the secure web authentication layer.

## Main Security Features

1. Secure user login

2. Email based OTP verification

3. Password hashing using Werkzeug

4. Strong password validation

5. Role based access control

6. Failed login attempt tracking

7. Temporary account lockout

8. Secure password reset

9. Limited session lifetime

10. Environment based secret management

11. Security alert emails

12. User profile management

## Web Interface

### Login Page

The login page allows the user to enter a username or email address, password, and assigned role.

The selected role must match the role stored for the user account.

<img width="893" height="668" alt="image" src="https://github.com/user-attachments/assets/60308d7c-62a7-43c8-be8a-1492049b9b56" />


### OTP Verification Page

After the login credentials are successfully verified, the system sends a six digit OTP to the user's registered email address.

The user must enter the correct OTP before accessing the protected application pages.
<img width="893" height="586" alt="image" src="https://github.com/user-attachments/assets/9a809a95-62ca-4411-868a-85e69b3bf9ca" />


### Forgot Password Page

The forgot password page allows users to start the password recovery process using their registered account information.

### Reset Password Page

The reset password page allows users to create a new password.

The new password must satisfy the defined password complexity requirements before it is accepted.

<img width="893" height="647" alt="image" src="https://github.com/user-attachments/assets/2daefe11-3a04-4086-a824-3df4921130aa" />


### Security Dashboard

The dashboard provides access to the web security functions available to the authenticated user.

The displayed content can be controlled according to the assigned user role.

<img width="897" height="976" alt="image" src="https://github.com/user-attachments/assets/7131b7dd-e81a-483c-ad1e-a9548f91aa1a" />


### User Profile Page

The profile page allows authenticated users to update their email address or password.

The current password must be verified before sensitive account information is changed.

<img width="908" height="1100" alt="image" src="https://github.com/user-attachments/assets/ffc5c727-2698-47e0-b945-c6acad8d6768" />


### Account Security

The application protects user accounts through OTP verification, password hashing, account lockout, session expiration, and role based access control.

## Authentication Workflow

The secure authentication workflow follows these steps:

1. The user enters a username or email address.

2. The user enters the account password.

3. The user selects the assigned role.

4. The system verifies the account information.

5. The system checks whether the account is temporarily locked.

6. The system verifies the submitted password against the stored password hash.

7. The system generates a six digit OTP.

8. The OTP is sent to the registered email address.

9. The user enters the received OTP.

10. The system verifies the OTP and its expiration time.

11. The authenticated session is created.

12. The user is redirected to the authorized web page.

## Password Security

Passwords are not stored as plain text.

Werkzeug password hashing functions are used to generate and verify password hashes.

New passwords must contain:

1. At least eight characters

2. At least one uppercase letter

3. At least one lowercase letter

4. At least one number

5. At least one special character

## OTP Security

The OTP mechanism provides an additional authentication layer.

The application applies the following OTP protections:

1. The OTP contains six digits.

2. The OTP is randomly generated.

3. The OTP is sent to the registered email address.

4. The OTP has a limited expiration period.

5. The OTP is stored as a hash in the session.

6. The OTP is removed after successful verification.

7. Incorrect or expired OTP codes are rejected.

## Account Lockout

The system tracks unsuccessful login attempts.

After five failed login attempts, the account is temporarily locked for ten minutes.

This mechanism helps reduce brute force attacks and automated password guessing.

A security alert email can also be sent to the registered email address when suspicious login activity is detected.

## Role Based Access Control

The application supports different user roles, including:

1. Clinician

2. Data Scientist

3. Administrator

The selected role during login must match the role stored in the account.

Protected pages can verify the authenticated user's role before allowing access.

This prevents users from accessing pages or functions that are not assigned to them.

## Session Security

The application creates a full authenticated session only after successful OTP verification.

Sessions have a limited lifetime.

Temporary authentication values are removed after the verification process.

The Flask secret key is loaded from an environment variable instead of being stored directly in the source code.

## Secret Management

Sensitive values must be stored in environment variables.

Example:

```env
STROKEWEB_SECRET_KEY=replace-with-a-secure-random-value
MAIL_USERNAME=your-email@example.com
MAIL_PASSWORD=your-email-application-password
```

The real `.env` file must not be uploaded to GitHub.

Only `.env.example` should be included in the public repository.

## Technologies

1. Python

2. Flask

3. Flask Mail

4. Werkzeug

5. SQLite

6. HTML

7. CSS

8. JavaScript

## Project Structure

```text
StrokeLens-Web-Security/
│
├── app.py
├── README.md
├── requirements.txt
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
└── screenshots/
    ├── login.png
    ├── otp-verification.png
    ├── forgot-password.png
    ├── reset-password.png
    ├── dashboard.png
    ├── profile.png
    └── account-security.png
```

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/StrokeLens-Web-Security.git
```

Open the project folder:

```bash
cd StrokeLens-Web-Security
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the environment on Windows:

```bash
.venv\Scripts\activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Create the local environment file:

```bash
copy .env.example .env
```

Add the required secret values to the `.env` file.

Run the application:

```bash
python app.py
```

Open the application in the browser:

```text
http://127.0.0.1:5000
```

## Security Notice

Before publishing the repository, make sure that screenshots do not display:

1. Real passwords

2. Real OTP codes

3. Personal email addresses

4. Secret keys

5. Private account information

6. Database records

7. Password reset tokens

8. Gmail application passwords

## Academic Context

This repository presents the web authentication and web security component of the StrokeLens graduation project developed at Mutah University.

The repository is intended for educational and demonstration purposes.

# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Teachers can sign up and unregister students after logging in

## Getting Started

1. Install the dependencies:

   ```
   pip install -r ../requirements.txt
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

### Teacher authentication

Teacher credentials are loaded from `teachers.json` by the backend. The sample
credential is `teacher` with password `mergington-teacher`; replace it before
deploying the application.

Set `SESSION_SECRET` to a long, random value in any shared or production
environment. The default value is intended only for local development.

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth/login`                                                     | Log in as a teacher                                                |
| POST   | `/auth/logout`                                                    | Log out the current teacher                                        |
| GET    | `/auth/me`                                                        | Get the current login status                                       |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up a student for an activity; teacher login required           |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student; teacher login required                    |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.

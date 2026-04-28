# Automatisiertes Bewertungssystem für Programmieraufgaben 

This project is a containerized microservice-based platform designed to automate the evaluation of programming tasks. It integrates GitLab CI/CD with custom feedback processors to provide students and instructors with real-time grading and performance analytics.

🏗 System Architecture
The system consists of four primary components that communicate via a REST API:

frontend-service: A React application providing a dashboard for students (viewing grades/feedback) and instructors (course management).

login-service: A dedicated Flask service that handles user authentication and role-based access control (Student vs. Instructor) using bcrypt for password security.

database-service: A Flask-based backend using SQLAlchemy ORM to manage PostgreSQL data for users, courses, and submission results.

GitLab-Projekt: The grading engine. It uses custom Python scripts (autograde.py and feedback_processor.py) to execute tests, calculate weighted points, and transmit results back to the database.

🚀 Key Features
Weighted Grading Logic: The system automatically extracts "points" from test docstrings to calculate final grades (e.g., 90% = 1.0, 80% = 2.0).

Automated Feedback Loop: On every code commit, the system triggers pytest and a linting process, generating a feedback.json that is pushed to the central database.

Detailed Analytics: For every assignment, the system stores specific test failures and achieved points, allowing instructors to give targeted guidance.

Containerized Infrastructure: Every service is Dockerized, and the system includes a pre-configured GitLab CE container for local repository management.

🛠 Tech Stack
Frontend: React.js, Tailwind CSS.

Backend: Python (Flask), REST API.

Database: PostgreSQL, SQLAlchemy ORM.

Automation: GitLab CI/CD, Docker, Pytest.

📂 Installation & Setup
Start GitLab and Infrastructure:
The main infrastructure (including GitLab) is managed via Docker Compose:
Bash
docker-compose -f GitLab/Docker-Compose.yml up -d
Service Configuration:
Ensure the login-service and database-service are running to handle user verification and data persistence.

Local Frontend Development:
Bash
cd frontend-service
npm install
npm start
🧪 Grading Workflow
Test Execution: autograde.py runs pytest and parses the output to find PASSED or FAILED status for each test case.

Point Calculation: Weights are extracted directly from the test files.

Result Processing: feedback_processor.py gathers lint results and grades, then formats them into a JSON structure for the database-service.

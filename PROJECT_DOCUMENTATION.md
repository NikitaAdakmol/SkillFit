# SkillFit - Complete Project Documentation

## 📋 Table of Contents
1. [Project Overview](#project-overview)
2. [Technology Stack](#technology-stack)
3. [Project Structure](#project-structure)
4. [How to Run the Project](#how-to-run-the-project)
5. [Project Concept & Flow](#project-concept--flow)
6. [Features & Functionality](#features--functionality)
7. [Database Schema](#database-schema)
8. [API Endpoints](#api-endpoints)
9. [Project Management Guide](#project-management-guide)
10. [Troubleshooting](#troubleshooting)

---

## 🎯 Project Overview

**SkillFit** is a comprehensive skill assessment and job matching platform designed to connect students with recruiters. The platform allows students to take skill assessments, receive job recommendations based on their skill level, and communicate directly with recruiters. Recruiters can post jobs, create custom assessments, view candidate results, and contact potential hires.

### Key Purpose
- **For Students**: Take skill assessments, discover job opportunities matching their skill level, and receive messages from recruiters
- **For Recruiters**: Post jobs, create custom quiz questions, assess candidates, and contact potential employees

---

## 🛠️ Technology Stack

### Backend
- **Language**: Java 17
- **Framework**: Spring Boot 3.3.4
- **Database**: MySQL (via XAMPP)
- **ORM**: Spring Data JPA / Hibernate
- **Build Tool**: Maven
- **Server**: Embedded Tomcat (Port 8080)

### Frontend
- **Language**: JavaScript (ES6+)
- **Framework**: React 19.2.0
- **Routing**: React Router DOM 7.9.6
- **HTTP Client**: Axios 1.13.2
- **UI Libraries**: 
  - Framer Motion 12.23.24 (animations)
  - Recharts 3.4.1 (data visualization)
- **Build Tool**: React Scripts 5.0.1
- **Styling**: CSS3 with modern glassmorphism design
- **Development Server**: Port 3000

### Database
- **Type**: MySQL
- **Default Database Name**: `skillfit`
- **Connection**: JDBC via MySQL Connector

---

## 📁 Project Structure

```
pro/
├── backend/                          # Spring Boot Backend
│   ├── src/
│   │   └── main/
│   │       ├── java/
│   │       │   └── com/example/
│   │       │       ├── Main.java              # Application entry point
│   │       │       ├── config/
│   │       │       │   └── DataInitializer.java
│   │       │       ├── controller/            # REST API Controllers
│   │       │       │   ├── HomeController.java
│   │       │       │   ├── JobController.java
│   │       │       │   ├── RecruiterAuthController.java
│   │       │       │   ├── RecruiterController.java
│   │       │       │   ├── StudentAuthController.java
│   │       │       │   ├── StudentController.java
│   │       │       │   ├── StudentMessageController.java
│   │       │       │   └── TestController.java
│   │       │       ├── model/                # Entity Models
│   │       │       │   ├── Job.java
│   │       │       │   ├── Message.java
│   │       │       │   ├── QuestionEntity.java
│   │       │       │   ├── Recruiter.java
│   │       │       │   ├── ResultEntity.java
│   │       │       │   └── Student.java
│   │       │       ├── repository/           # Data Access Layer
│   │       │       │   ├── JobRepository.java
│   │       │       │   ├── MessageRepository.java
│   │       │       │   ├── QuestionRepository.java
│   │       │       │   ├── RecruiterRepository.java
│   │       │       │   ├── ResultRepository.java
│   │       │       │   └── StudentRepository.java
│   │       │       └── exception/
│   │       │           └── GlobalExceptionHandler.java
│   │       └── resources/
│   │           └── application.properties    # Configuration
│   └── pom.xml                               # Maven dependencies
│
└── skillfit-frontend/                # React Frontend
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── api/
    │   │   └── apiService.js         # API service functions
    │   ├── components/
    │   │   ├── Dashboard.jsx
    │   │   ├── Quiz.js               # Quiz component
    │   │   ├── Recommendation.jsx
    │   │   ├── RecruiterDashboard.jsx
    │   │   └── StudentWebsite.jsx
    │   ├── pages/
    │   │   ├── Auth.jsx
    │   │   ├── Home.jsx              # Landing page
    │   │   ├── RecruiterAuth.jsx
    │   │   ├── Result.jsx
    │   │   ├── UnifiedAuth.jsx
    │   │   └── student/
    │   │       └── HomePage.jsx
    │   ├── App.js                    # Main app component
    │   ├── ProtectedRoute.jsx       # Route protection
    │   └── index.js                 # Entry point
    └── package.json                 # NPM dependencies
```

---

## 🚀 How to Run the Project

### Prerequisites
1. **Java Development Kit (JDK) 17** or higher
2. **Node.js** (v14 or higher) and **npm**
3. **XAMPP** (for MySQL database)
4. **Maven** (usually comes with IDE or can be installed separately)
5. **IDE** (IntelliJ IDEA, Eclipse, or VS Code recommended)

### Step 1: Database Setup

1. **Start XAMPP**
   - Open XAMPP Control Panel
   - Start **Apache** and **MySQL** services

2. **Create Database**
   - Open phpMyAdmin (http://localhost/phpmyadmin)
   - Create a new database named `skillfit`
   - The application will auto-create tables on first run (due to `spring.jpa.hibernate.ddl-auto=update`)

3. **Configure Database Connection**
   - Edit `backend/src/main/resources/application.properties`
   - Update if needed:
     ```properties
     spring.datasource.url=jdbc:mysql://localhost:3306/skillfit
     spring.datasource.username=root
     spring.datasource.password=        # Leave blank if no password
     ```

### Step 2: Run Backend (Spring Boot)

**Option A: Using IDE (Recommended)**
1. Open the `backend` folder in your IDE (IntelliJ IDEA/Eclipse)
2. Wait for Maven to download dependencies
3. Locate `Main.java` in `com.example` package
4. Right-click → Run `Main.main()`
5. Wait for: `✅ SkillFit Backend is running...`
6. Backend runs on: **http://localhost:8080**

**Option B: Using Command Line**
```bash
cd backend
mvn spring-boot:run
```

**Verify Backend is Running:**
- Open browser: http://localhost:8080
- You should see a response or no error

### Step 3: Run Frontend (React)

1. **Open Terminal/Command Prompt**
2. **Navigate to frontend directory:**
   ```bash
   cd skillfit-frontend
   ```

3. **Install Dependencies** (First time only):
   ```bash
   npm install
   ```

4. **Start Development Server:**
   ```bash
   npm start
   ```

5. **Frontend runs on: http://localhost:3000**
   - Browser should open automatically
   - If not, manually open http://localhost:3000

### Step 4: Access the Application

1. **Landing Page**: http://localhost:3000
2. **Student Login/Register**: http://localhost:3000/auth?type=student
3. **Recruiter Login/Register**: http://localhost:3000/auth?type=recruiter

---

## 🔄 Project Concept & Flow

### System Architecture

```
┌─────────────────┐         ┌─────────────────┐         ┌─────────────────┐
│   React Frontend │ ◄─────► │  Spring Boot API │ ◄─────► │   MySQL Database │
│   (Port 3000)    │  HTTP   │   (Port 8080)    │   JDBC   │   (Port 3306)    │
└─────────────────┘         └─────────────────┘         └─────────────────┘
```

### User Flow

#### **Student Flow:**
1. **Registration/Login** → Student creates account or logs in
2. **Take Assessment** → Student takes skill assessment quiz
3. **View Results** → System calculates score and assigns skill level:
   - **Beginner**: 0-25% correct
   - **Intermediate**: 26-75% correct
   - **Advanced**: 76-100% correct
4. **Job Recommendations** → System shows jobs matching student's skill level
5. **View Messages** → Student receives messages from recruiters
6. **Apply/Contact** → Student can view job details and respond to messages

#### **Recruiter Flow:**
1. **Registration/Login** → Recruiter creates account or logs in
2. **Post Jobs** → Recruiter creates job postings with:
   - Job Role (e.g., "Frontend Developer")
   - Skill Level (Beginner/Intermediate/Expert)
   - Job Description
3. **Create Assessments** → Recruiter creates custom quiz questions:
   - Can link questions to specific jobs
   - Or create general questions for all jobs
4. **View Candidates** → Recruiter sees all registered students with:
   - Assessment scores
   - Skill levels
   - Assessment history
5. **Contact Candidates** → Recruiter sends messages to students
6. **Manage Jobs** → Recruiter can edit/delete job postings

### Data Flow

```
Student Registration
    ↓
Student Takes Quiz
    ↓
Answers Submitted → Backend Calculates Score
    ↓
Score Saved → Student Level Updated
    ↓
Job Recommendations Based on Level
    ↓
Recruiter Views Candidates
    ↓
Recruiter Sends Message
    ↓
Student Receives Message
```

---

## ✨ Features & Functionality

### Student Features
- ✅ **User Authentication**: Register and login
- ✅ **Skill Assessment**: Take multiple-choice quiz
- ✅ **Result Display**: View score, level, and performance
- ✅ **Job Recommendations**: See jobs matching skill level
- ✅ **Message System**: Receive and view messages from recruiters
- ✅ **Dashboard**: View all assessments, jobs, and messages
- ✅ **Profile Management**: View and update profile

### Recruiter Features
- ✅ **User Authentication**: Register and login
- ✅ **Job Management**: Create, edit, and delete job postings
- ✅ **Question Management**: Create custom quiz questions
- ✅ **Candidate Viewing**: See all students with their assessment results
- ✅ **Candidate Details**: View detailed assessment history
- ✅ **Messaging**: Send messages to candidates
- ✅ **Dashboard**: Overview of jobs, candidates, and statistics
- ✅ **Profile Management**: Update recruiter profile

### System Features
- ✅ **Skill Level Calculation**: Automatic level assignment based on score
- ✅ **Job-Level Matching**: Jobs recommended based on student skill level
- ✅ **Question Linking**: Questions can be linked to specific jobs
- ✅ **Message Tracking**: Unread message count for students
- ✅ **Assessment History**: Track all previous assessments
- ✅ **Responsive Design**: Modern glassmorphism UI design

---

## 🗄️ Database Schema

### Tables

#### **students**
| Column | Type | Description |
|--------|------|-------------|
| id | BIGINT (PK) | Auto-increment primary key |
| name | VARCHAR | Student's full name |
| email | VARCHAR | Student's email (unique) |
| level | VARCHAR | Skill level (Beginner/Intermediate/Advanced) |
| score | INT | Latest assessment score |

#### **recruiters**
| Column | Type | Description |
|--------|------|-------------|
| id | BIGINT (PK) | Auto-increment primary key |
| name | VARCHAR | Recruiter's full name |
| email | VARCHAR | Recruiter's email (unique) |
| password | VARCHAR | Encrypted password |

#### **jobs**
| Column | Type | Description |
|--------|------|-------------|
| id | BIGINT (PK) | Auto-increment primary key |
| role | VARCHAR(500) | Job title/role |
| level | VARCHAR(50) | Required skill level |
| description | TEXT | Job description |

#### **question_entity**
| Column | Type | Description |
|--------|------|-------------|
| id | BIGINT (PK) | Auto-increment primary key |
| question_text | TEXT | The question |
| options | JSON/ARRAY | Array of answer options |
| correct_answer | VARCHAR | Correct answer |
| job_id | BIGINT (FK) | Optional: linked job ID |
| is_active | BOOLEAN | Whether question is active |

#### **result_entity**
| Column | Type | Description |
|--------|------|-------------|
| id | BIGINT (PK) | Auto-increment primary key |
| student_id | BIGINT (FK) | Reference to student |
| score | INT | Assessment score |
| level | VARCHAR | Assigned skill level |
| taken_at | DATETIME | When assessment was taken |

#### **messages**
| Column | Type | Description |
|--------|------|-------------|
| id | BIGINT (PK) | Auto-increment primary key |
| recruiter_id | BIGINT (FK) | Reference to recruiter |
| student_id | BIGINT (FK) | Reference to student |
| subject | VARCHAR | Message subject |
| message | TEXT | Message content |
| sent_at | DATETIME | When message was sent |
| is_read | BOOLEAN | Read status |

---

## 🌐 API Endpoints

### Base URL: `http://localhost:8080`

### Authentication Endpoints

#### Student Authentication
- `POST /api/auth/register` - Register new student
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com"
  }
  ```

- `POST /api/auth/login` - Student login
  ```json
  {
    "email": "john@example.com"
  }
  ```

#### Recruiter Authentication
- `POST /api/recruiter/register` - Register new recruiter
- `POST /api/recruiter/login` - Recruiter login

### Test/Assessment Endpoints

- `GET /api/test/questions` - Get questions (for students)
  - Query param: `?jobId=1` (optional)

- `GET /api/test/questions/with-answers` - Get questions with answers (for recruiters)

- `POST /api/test/questions/create` - Create new question
  ```json
  {
    "questionText": "What is React?",
    "options": ["Framework", "Library", "Language", "Tool"],
    "correctAnswer": "Library",
    "jobId": 1  // optional
  }
  ```

- `POST /api/test/submit?studentId=1` - Submit quiz answers
  ```json
  {
    "answers": {
      "1": "Java",
      "2": "Frontend"
    }
  }
  ```

### Job Endpoints

- `GET /api/jobs/all` - Get all jobs
- `GET /api/jobs/recommend/{level}` - Get jobs by level
- `POST /api/jobs/create` - Create job
  ```json
  {
    "role": "Frontend Developer",
    "level": "Intermediate",
    "description": "Job description here"
  }
  ```
- `PUT /api/jobs/update/{id}` - Update job
- `DELETE /api/jobs/delete/{id}` - Delete job

### Student Endpoints

- `GET /api/student/result/{id}` - Get student result
- `GET /api/student/message/received/{studentId}` - Get received messages
- `GET /api/student/message/unread-count/{studentId}` - Get unread count

### Recruiter Endpoints

- `GET /api/recruiter/students` - Get all students
- `GET /api/recruiter/students/{id}` - Get student details
- `POST /api/recruiter/message/send` - Send message to student
  ```json
  {
    "recruiterId": 1,
    "studentId": 1,
    "subject": "Job Opportunity",
    "message": "We'd like to interview you..."
  }
  ```

---

## 📊 Project Management Guide

### For Developers

#### **Adding New Features**

1. **Backend (Java/Spring Boot)**
   - Create model class in `model/` package
   - Create repository interface in `repository/` package
   - Create controller in `controller/` package
   - Add API endpoints with proper CORS configuration

2. **Frontend (React)**
   - Create component in `components/` or `pages/`
   - Add API service function in `api/apiService.js`
   - Add route in `App.js`
   - Update navigation if needed

#### **Code Organization**

- **Backend**: Follow MVC pattern
  - Models: Data entities
  - Repositories: Data access
  - Controllers: Business logic and API endpoints

- **Frontend**: Component-based architecture
  - Pages: Full page components
  - Components: Reusable UI components
  - API Service: Centralized API calls

#### **Best Practices**

1. **Error Handling**
   - Backend: Use `GlobalExceptionHandler`
   - Frontend: Use try-catch blocks and show user-friendly messages

2. **Security**
   - Currently uses localStorage for session (can be improved with JWT)
   - Add input validation
   - Sanitize user inputs

3. **Performance**
   - Use React hooks efficiently
   - Implement pagination for large lists
   - Optimize database queries

### For Project Owners

#### **Deployment Considerations**

1. **Production Database**
   - Use production MySQL server
   - Set strong passwords
   - Enable SSL connections

2. **Environment Variables**
   - Move hardcoded values to environment variables
   - Use different configs for dev/prod

3. **Build Process**
   - Backend: `mvn clean package` → creates JAR file
   - Frontend: `npm run build` → creates production build

4. **Hosting**
   - Backend: Deploy JAR to cloud (AWS, Heroku, etc.)
   - Frontend: Deploy build to static hosting (Netlify, Vercel, etc.)

#### **Maintenance Tasks**

- Regular database backups
- Monitor API performance
- Update dependencies regularly
- Review and fix security vulnerabilities

---

## 🔧 Troubleshooting

### Common Issues

#### **Backend Won't Start**
- ✅ Check if MySQL is running in XAMPP
- ✅ Verify database `skillfit` exists
- ✅ Check `application.properties` credentials
- ✅ Ensure port 8080 is not in use
- ✅ Check Java version: `java -version` (should be 17+)

#### **Frontend Won't Start**
- ✅ Check Node.js version: `node -v` (should be 14+)
- ✅ Delete `node_modules` and run `npm install` again
- ✅ Check if port 3000 is available
- ✅ Clear browser cache

#### **Database Connection Errors**
- ✅ Verify MySQL is running
- ✅ Check database name matches `application.properties`
- ✅ Verify username/password
- ✅ Check if database exists in phpMyAdmin

#### **CORS Errors**
- ✅ Ensure backend CORS is configured: `@CrossOrigin(origins = "http://localhost:3000")`
- ✅ Check if backend is running on port 8080
- ✅ Verify frontend is calling correct API URL

#### **API Calls Failing**
- ✅ Check browser console for errors
- ✅ Verify backend is running
- ✅ Check API endpoint URLs in `apiService.js`
- ✅ Verify request/response format matches

### Debugging Tips

1. **Backend Logs**: Check console output for Spring Boot logs
2. **Frontend Console**: Open browser DevTools (F12) → Console tab
3. **Network Tab**: Check API requests/responses in browser DevTools
4. **Database**: Use phpMyAdmin to verify data

---

## 📝 Additional Notes

### Current Limitations

- No password encryption (can be added with BCrypt)
- No email verification
- No file upload functionality
- No real-time notifications
- Simple authentication (localStorage-based)

### Future Enhancements

- JWT-based authentication
- Email notifications
- File upload for resumes
- Advanced search and filtering
- Analytics dashboard
- Multi-language support
- Mobile app version

---

## 📞 Support & Contact

For questions or issues:
1. Check this documentation
2. Review code comments
3. Check error logs
4. Verify all prerequisites are installed

---

## 📄 License

This project is created for educational and commercial purposes.

---

**Last Updated**: 2024
**Version**: 1.0.0

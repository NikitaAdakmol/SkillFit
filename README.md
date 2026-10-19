# SkillFit - Skill Assessment & Job Matching Platform

<div align="center">

![SkillFit](https://img.shields.io/badge/SkillFit-v1.0.0-blue)
![Java](https://img.shields.io/badge/Java-17-orange)
![React](https://img.shields.io/badge/React-19.2.0-blue)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.3.4-green)
![MySQL](https://img.shields.io/badge/MySQL-8.0-blue)

**A comprehensive platform connecting students with recruiters through skill assessments and job matching**

[Quick Start](#-quick-start) • [Documentation](#-documentation) • [Features](#-features) • [Tech Stack](#-tech-stack)

</div>

---

## 📖 Overview

**SkillFit** is a full-stack web application that bridges the gap between students seeking opportunities and recruiters looking for talent. Students can take skill assessments, receive personalized job recommendations, and connect with recruiters. Recruiters can post jobs, create custom assessments, evaluate candidates, and reach out to potential hires.

### Key Features
- 🎯 **Skill Assessment System** - Multiple-choice quizzes with automatic scoring
- 💼 **Job Matching** - Jobs recommended based on skill level
- 📊 **Candidate Management** - Recruiters can view and assess all candidates
- 💬 **Messaging System** - Direct communication between recruiters and students
- 📈 **Progress Tracking** - Students can track their assessment history
- 🎨 **Modern UI** - Beautiful glassmorphism design

---

## 🚀 Quick Start

### Prerequisites
- Java JDK 17+
- Node.js 14+
- XAMPP (for MySQL)
- Maven (usually included with IDE)

### Installation

1. **Start MySQL Database**
   ```bash
   # Open XAMPP → Start MySQL
   # Create database: skillfit (or auto-created)
   ```

2. **Start Backend**
   ```bash
   cd backend
   # Using IDE: Run Main.java
   # OR using Maven:
   mvn spring-boot:run
   ```

3. **Start Frontend**
   ```bash
   cd skillfit-frontend
   npm install
   npm start
   ```

4. **Access Application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8080

📖 **For detailed setup instructions, see [QUICK_START_GUIDE.md](QUICK_START_GUIDE.md)**

---

## 📚 Documentation

- **[PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md)** - Complete project documentation
  - Technology stack details
  - Project structure
  - API endpoints
  - Database schema
  - Troubleshooting guide

- **[QUICK_START_GUIDE.md](QUICK_START_GUIDE.md)** - Quick setup guide

---

## 🛠️ Tech Stack

### Backend
- **Java 17** - Programming language
- **Spring Boot 3.3.4** - Framework
- **Spring Data JPA** - Database ORM
- **MySQL** - Database
- **Maven** - Build tool

### Frontend
- **React 19.2.0** - UI framework
- **React Router** - Routing
- **Axios** - HTTP client
- **Framer Motion** - Animations
- **Recharts** - Data visualization

---

## 📁 Project Structure

```
pro/
├── backend/                 # Spring Boot Backend
│   ├── src/main/java/      # Java source code
│   └── pom.xml             # Maven dependencies
│
├── skillfit-frontend/      # React Frontend
│   ├── src/                # React source code
│   └── package.json       # NPM dependencies
│
├── PROJECT_DOCUMENTATION.md    # Full documentation
├── QUICK_START_GUIDE.md        # Quick setup guide
└── README.md                   # This file
```

---

## ✨ Features

### For Students
- ✅ User registration and authentication
- ✅ Take skill assessment quizzes
- ✅ View assessment results and skill level
- ✅ Get job recommendations based on skill level
- ✅ Receive and view messages from recruiters
- ✅ Track assessment history

### For Recruiters
- ✅ User registration and authentication
- ✅ Create, edit, and delete job postings
- ✅ Create custom quiz questions (job-specific or general)
- ✅ View all candidates with assessment results
- ✅ View detailed candidate assessment history
- ✅ Send messages to candidates
- ✅ Dashboard with statistics

---

## 🔄 How It Works

1. **Student Flow:**
   - Register/Login → Take Assessment → View Results → Get Job Recommendations → Receive Messages

2. **Recruiter Flow:**
   - Register/Login → Post Jobs → Create Questions → View Candidates → Send Messages

3. **System Flow:**
   - Assessment scores determine skill level (Beginner/Intermediate/Advanced)
   - Jobs are matched based on skill level
   - Recruiters can contact students directly

---

## 🌐 API Endpoints

### Base URL: `http://localhost:8080`

**Key Endpoints:**
- `POST /api/auth/register` - Student registration
- `POST /api/auth/login` - Student login
- `GET /api/test/questions` - Get quiz questions
- `POST /api/test/submit` - Submit quiz answers
- `GET /api/jobs/all` - Get all jobs
- `GET /api/jobs/recommend/{level}` - Get jobs by level
- `GET /api/recruiter/students` - Get all candidates
- `POST /api/recruiter/message/send` - Send message

📖 **See [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md) for complete API documentation**

---

## 🗄️ Database

**MySQL Database:** `skillfit`

**Main Tables:**
- `students` - Student information and latest scores
- `recruiters` - Recruiter accounts
- `jobs` - Job postings
- `question_entity` - Quiz questions
- `result_entity` - Assessment results
- `messages` - Messages between recruiters and students

---

## 🎯 Use Cases

### For College Students
- Take skill assessments to evaluate your knowledge
- Discover job opportunities matching your skill level
- Connect with recruiters directly
- Track your progress over time

### For Recruiters/Companies
- Post job openings with skill level requirements
- Create custom assessments for specific roles
- Evaluate candidates based on assessment results
- Contact qualified candidates directly

---

## 🔧 Configuration

### Backend Configuration
File: `backend/src/main/resources/application.properties`

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/skillfit
spring.datasource.username=root
spring.datasource.password=
server.port=8080
```

### Frontend Configuration
File: `skillfit-frontend/src/api/apiService.js`

```javascript
const API = "http://localhost:8080";
```

---

## ⚠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| Backend won't start | Check MySQL is running in XAMPP |
| Frontend won't start | Run `npm install` first |
| Database connection error | Verify database exists and credentials are correct |
| CORS errors | Ensure backend is running on port 8080 |
| Port already in use | Change port or kill existing process |

📖 **See [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md) for detailed troubleshooting**

---

## 📝 Project Information

- **Project Name:** SkillFit
- **Version:** 1.0.0
- **Purpose:** Skill assessment and job matching platform
- **Target Audience:** College students and recruiters

---

## 📄 License

This project is created for educational and commercial purposes.

---

## 🤝 Contributing

This is a complete project ready for deployment. For modifications:
1. Review the code structure
2. Follow existing patterns
3. Test thoroughly before deployment

---

## 📞 Support

For detailed information:
- Read [PROJECT_DOCUMENTATION.md](PROJECT_DOCUMENTATION.md)
- Check [QUICK_START_GUIDE.md](QUICK_START_GUIDE.md)
- Review code comments

---

<div align="center">

**Built with ❤️ for connecting talent with opportunities**

[Back to Top](#skillfit---skill-assessment--job-matching-platform)

</div>

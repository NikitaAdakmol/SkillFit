# SkillFit - Technical Architecture

## 🏗️ System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                            │
│                    (React Frontend - Port 3000)                 │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐        │
│  │   Student    │  │  Recruiter    │  │   Landing    │        │
│  │   Dashboard  │  │  Dashboard   │  │     Page     │        │
│  └──────────────┘  └──────────────┘  └──────────────┘        │
│         │                  │                  │                │
│         └──────────────────┼──────────────────┘                │
│                            │                                    │
│                    ┌───────▼────────┐                          │
│                    │  API Service   │                          │
│                    │   (Axios)      │                          │
│                    └───────┬────────┘                          │
└────────────────────────────┼────────────────────────────────────┘
                             │ HTTP/REST
                             │
┌────────────────────────────▼────────────────────────────────────┐
│                      API LAYER                                  │
│              (Spring Boot Backend - Port 8080)                   │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │                    Controllers                            │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐   │  │
│  │  │   Student    │  │  Recruiter   │  │     Test     │   │  │
│  │  │  Controller  │  │  Controller  │  │  Controller  │   │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘   │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐   │  │
│  │  │     Job      │  │    Message   │  │     Auth     │   │  │
│  │  │  Controller  │  │  Controller  │  │  Controller   │   │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘   │  │
│  └──────────────────────────────────────────────────────────┘  │
│                            │                                    │
│  ┌────────────────────────▼──────────────────────────────────┐  │
│  │                  Business Logic                            │  │
│  │  • Score Calculation                                       │  │
│  │  • Level Assignment (Beginner/Intermediate/Advanced)      │  │
│  │  • Job Matching Algorithm                                 │  │
│  │  • Message Routing                                        │  │
│  └────────────────────────┬──────────────────────────────────┘  │
│                            │                                    │
│  ┌────────────────────────▼──────────────────────────────────┐  │
│  │                  Repository Layer                         │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │  │
│  │  │   Student    │  │  Recruiter   │  │     Job     │     │  │
│  │  │  Repository  │  │  Repository │  │  Repository │     │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘     │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │  │
│  │  │  Question    │  │   Result     │  │   Message    │     │  │
│  │  │  Repository  │  │  Repository  │  │  Repository  │     │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘     │  │
│  └────────────────────────┬──────────────────────────────────┘  │
└────────────────────────────┼────────────────────────────────────┘
                             │ JDBC
                             │
┌────────────────────────────▼────────────────────────────────────┐
│                    DATA LAYER                                   │
│                  (MySQL Database)                               │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │   students   │  │  recruiters  │  │    jobs     │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │question_entity│  │result_entity │  │  messages   │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔄 Request Flow

### Student Taking Assessment

```
1. Student clicks "Take Quiz"
   ↓
2. Frontend: Quiz.js component loads
   ↓
3. API Call: GET /api/test/questions
   ↓
4. Backend: TestController.getQuestions()
   ↓
5. Repository: QuestionRepository.findByIsActiveTrue()
   ↓
6. Database: SELECT * FROM question_entity WHERE is_active = true
   ↓
7. Response: Questions (without answers) sent to frontend
   ↓
8. Student answers questions
   ↓
9. API Call: POST /api/test/submit?studentId=1
   ↓
10. Backend: TestController.submitTest()
    ↓
11. Business Logic:
    - Compare answers with correct answers
    - Calculate score
    - Determine level (Beginner/Intermediate/Advanced)
    ↓
12. Repository: Save result to result_entity
    ↓
13. Repository: Update student level and score
    ↓
14. Response: Score, level, and message sent to frontend
    ↓
15. Frontend: Display results page
```

### Recruiter Viewing Candidates

```
1. Recruiter clicks "Candidates"
   ↓
2. Frontend: RecruiterDashboard component loads
   ↓
3. API Call: GET /api/recruiter/students
   ↓
4. Backend: RecruiterController.getAllStudents()
   ↓
5. Repository: StudentRepository.findAll()
   ↓
6. Repository: ResultRepository.findByStudentIdOrderByTakenAtDesc()
   ↓
7. Business Logic: Combine student data with latest results
   ↓
8. Response: List of students with scores and levels
   ↓
9. Frontend: Display candidates list
```

---

## 🗂️ Component Structure

### Frontend Components

```
App.js (Root)
├── Home.jsx (Landing Page)
├── UnifiedAuth.jsx (Login/Register)
├── StudentWebsite.jsx
│   ├── StudentSidebar
│   ├── TopBar
│   ├── HomePage
│   ├── Quiz.js
│   └── Result.jsx
└── RecruiterDashboard.jsx
    ├── Sidebar
    ├── TopBar
    ├── JobManagement
    ├── TestManagement
    ├── StudentsList
    └── ProfileManagement
```

### Backend Structure

```
com.example
├── Main.java (Application Entry)
├── config/
│   └── DataInitializer.java
├── controller/ (REST API Endpoints)
│   ├── StudentAuthController
│   ├── RecruiterAuthController
│   ├── TestController
│   ├── JobController
│   ├── RecruiterController
│   └── StudentMessageController
├── model/ (JPA Entities)
│   ├── Student
│   ├── Recruiter
│   ├── Job
│   ├── QuestionEntity
│   ├── ResultEntity
│   └── Message
├── repository/ (Data Access)
│   ├── StudentRepository
│   ├── RecruiterRepository
│   ├── JobRepository
│   ├── QuestionRepository
│   ├── ResultRepository
│   └── MessageRepository
└── exception/
    └── GlobalExceptionHandler
```

---

## 🔐 Authentication Flow

### Current Implementation (Simple)

```
1. User registers/login
   ↓
2. Backend returns userId and name
   ↓
3. Frontend stores in localStorage:
   - studentId / recruiterId
   - username / recruiterName
   ↓
4. Protected routes check localStorage
   ↓
5. If not authenticated → redirect to /auth
```

### Recommended Enhancement (JWT)

```
1. User registers/login
   ↓
2. Backend generates JWT token
   ↓
3. Frontend stores token in localStorage
   ↓
4. All API requests include token in header:
   Authorization: Bearer <token>
   ↓
5. Backend validates token on each request
   ↓
6. Token expires after set time
```

---

## 📊 Data Flow Diagrams

### Assessment Submission Flow

```
┌──────────┐         ┌──────────┐         ┌──────────┐
│ Student  │────────▶│ Frontend │────────▶│ Backend │
│          │ Answers │          │ Submit  │          │
└──────────┘         └──────────┘         └────┬─────┘
                                                │
                                                ▼
                                         ┌──────────────┐
                                         │ Calculate    │
                                         │ Score & Level│
                                         └──────┬───────┘
                                                │
                                                ▼
                                         ┌──────────────┐
                                         │ Save Result  │
                                         │ Update Student│
                                         └──────┬───────┘
                                                │
                                                ▼
┌──────────┐         ┌──────────┐         ┌──────────┐
│ Student  │◀────────│ Frontend │◀────────│ Backend │
│          │ Results │          │ Response│          │
└──────────┘         └──────────┘         └──────────┘
```

### Job Matching Flow

```
┌──────────┐         ┌──────────┐         ┌──────────┐
│ Student  │────────▶│ Frontend │────────▶│ Backend │
│          │ Request │          │ GET     │          │
│          │ Jobs    │          │ /jobs/  │          │
└──────────┘         └──────────┘ recommend/level  └────┬─────┘
                                                           │
                                                           ▼
                                                    ┌──────────────┐
                                                    │ Query Jobs   │
                                                    │ WHERE level =│
                                                    │ student.level│
                                                    └──────┬───────┘
                                                           │
                                                           ▼
┌──────────┐         ┌──────────┐         ┌──────────┐
│ Student  │◀────────│ Frontend │◀────────│ Backend │
│          │ Jobs    │          │ Jobs    │          │
└──────────┘         └──────────┘         └──────────┘
```

---

## 🔌 API Communication

### Request/Response Format

**Request Example:**
```javascript
// Frontend
axios.post('http://localhost:8080/api/test/submit?studentId=1', {
  answers: {
    "1": "Java",
    "2": "Frontend"
  }
})
```

**Response Example:**
```json
{
  "score": 3,
  "totalQuestions": 4,
  "level": "Intermediate",
  "message": "Test submitted successfully!"
}
```

### Error Handling

```javascript
try {
  const response = await apiCall();
  // Handle success
} catch (error) {
  if (error.response) {
    // Server responded with error
    console.error(error.response.data);
  } else {
    // Network error
    console.error(error.message);
  }
}
```

---

## 🗄️ Database Relationships

```
students (1) ──────< (many) result_entity
    │
    │
    └───────< (many) messages >─────── (many) recruiters

jobs (1) ──────< (many) question_entity
```

**Key Relationships:**
- One Student → Many Results
- One Student → Many Messages
- One Recruiter → Many Messages
- One Job → Many Questions (optional)
- One Question → One Job (optional, nullable)

---

## 🚀 Deployment Architecture

### Development
```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   React     │───▶│  Spring Boot│───▶│   MySQL     │
│  (Port 3000)│    │  (Port 8080)│    │  (Port 3306)│
└─────────────┘    └─────────────┘    └─────────────┘
```

### Production (Recommended)
```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   CDN/      │───▶│  Cloud      │───▶│   Cloud     │
│   Static    │    │  Backend    │    │   Database  │
│   Hosting   │    │  (AWS/      │    │   (RDS)     │
│             │    │   Heroku)   │    │             │
└─────────────┘    └─────────────┘    └─────────────┘
```

---

## 🔒 Security Considerations

### Current State
- ✅ CORS configured
- ✅ Input validation in controllers
- ⚠️ Simple localStorage authentication
- ⚠️ No password encryption
- ⚠️ No HTTPS (development only)

### Recommended Enhancements
- [ ] JWT token-based authentication
- [ ] Password hashing (BCrypt)
- [ ] HTTPS/SSL certificates
- [ ] Rate limiting
- [ ] Input sanitization
- [ ] SQL injection prevention (already handled by JPA)
- [ ] XSS protection

---

## 📈 Performance Optimization

### Current Optimizations
- React component memoization
- Database indexing (via JPA)
- Connection pooling (Spring Boot default)

### Recommended Enhancements
- [ ] Implement pagination for large lists
- [ ] Add caching layer (Redis)
- [ ] Optimize database queries
- [ ] Implement lazy loading
- [ ] Compress API responses
- [ ] CDN for static assets

---

## 🧪 Testing Strategy

### Unit Tests
- Backend: JUnit tests for controllers and services
- Frontend: Jest tests for components

### Integration Tests
- API endpoint testing
- Database integration tests

### E2E Tests
- User flow testing (Cypress/Selenium)

---

## 📝 Notes

- **Current Version**: 1.0.0
- **Architecture Pattern**: MVC (Model-View-Controller)
- **API Style**: RESTful
- **State Management**: React Hooks (useState, useEffect)
- **Database**: Relational (MySQL)

---

**Last Updated**: 2024

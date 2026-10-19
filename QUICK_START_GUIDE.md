# SkillFit - Quick Start Guide

## 🚀 Quick Setup (5 Minutes)

### Step 1: Start Database
1. Open **XAMPP Control Panel**
2. Click **Start** for **Apache** and **MySQL**
3. Open **phpMyAdmin** (http://localhost/phpmyadmin)
4. Create database: `skillfit` (or it will auto-create)

### Step 2: Start Backend
**Using IDE (Easiest):**
1. Open `backend` folder in IntelliJ IDEA or Eclipse
2. Wait for Maven to download dependencies
3. Run `Main.java` (Right-click → Run)
4. ✅ Wait for: "SkillFit Backend is running..."

**Using Command Line:**
```bash
cd backend
mvn spring-boot:run
```

**Backend URL:** http://localhost:8080

### Step 3: Start Frontend
```bash
cd skillfit-frontend
npm install    # First time only
npm start
```

**Frontend URL:** http://localhost:3000 (opens automatically)

### Step 4: Test the Application
1. Go to http://localhost:3000
2. Click "I'm a Student" → Register
3. Take the quiz
4. View results and job recommendations

---

## 📋 Prerequisites Checklist

- [ ] Java JDK 17+ installed (`java -version`)
- [ ] Node.js 14+ installed (`node -v`)
- [ ] XAMPP installed and MySQL running
- [ ] Port 8080 available (backend)
- [ ] Port 3000 available (frontend)

---

## 🔧 Configuration

### Database Settings
File: `backend/src/main/resources/application.properties`

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/skillfit
spring.datasource.username=root
spring.datasource.password=        # Leave blank if no password
```

### API Base URL
File: `skillfit-frontend/src/api/apiService.js`

```javascript
const API = "http://localhost:8080";
```

---

## 🎯 Test Accounts

### Create Test Student
1. Go to http://localhost:3000/auth?type=student
2. Register with any email (e.g., `student@test.com`)
3. Login and take quiz

### Create Test Recruiter
1. Go to http://localhost:3000/auth?type=recruiter
2. Register with any email (e.g., `recruiter@test.com`)
3. Login and create jobs

---

## ⚠️ Common Issues

| Problem | Solution |
|---------|----------|
| Backend won't start | Check MySQL is running in XAMPP |
| Frontend won't start | Run `npm install` first |
| Database error | Create `skillfit` database in phpMyAdmin |
| CORS error | Ensure backend is running on port 8080 |
| Port already in use | Change port in `application.properties` or kill process |

---

## 📚 Full Documentation

See `PROJECT_DOCUMENTATION.md` for complete details.

---

**Need Help?** Check the full documentation or review error messages in console.

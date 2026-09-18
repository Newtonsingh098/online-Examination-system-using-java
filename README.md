# 📝 Online Examination System

> A professional Java Swing desktop application for conducting timed multiple-choice examinations with automatic evaluation and instant results.

![Java](https://img.shields.io/badge/Java-17%2B-orange?style=for-the-badge&logo=openjdk)
![Java Swing](https://img.shields.io/badge/GUI-Java%20Swing-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

## 📌 Overview

The **Online Examination System** is a Java-based desktop application that simulates a real-world examination workflow. Students can log in, manage their profile, start a timed examination, navigate through MCQs, submit answers, and receive an automatically calculated result.

This project was developed as part of my **Java Development Internship at Oasis Infobyte**, focusing on Core Java, Object-Oriented Programming, Java Swing GUI development, event handling, and problem solving.

## ✨ Features

-  Student login and authentication
-  Profile and password management
-  Multiple-choice examination interface
-  30-minute countdown timer
-  Previous / Next question navigation
-  Automatic answer evaluation
-  Instant score calculation
-  Correct, incorrect, and unanswered breakdown
-  Automatic submission when time expires
-  Java Swing graphical interface
-  Logout and safe exit handling

## 🛠️ Technologies & Concepts

| Technology / Concept | Usage |
|---|---|
| Java | Core application development |
| Java Swing | Desktop graphical interface |
| OOP | Application structure and data modelling |
| CardLayout | Screen navigation |
| GridBagLayout / BorderLayout | GUI layout |
| Swing Timer | Real-time examination countdown |
| Event Handling | User interaction |
| Collections | Question management |

## 🧠 Application Flow

```text
Application Start → Student Login → Profile → Start Exam
        ↓
8 MCQs + 30-Minute Timer
        ↓
Submit / Time Expires
        ↓
Automatic Evaluation
        ↓
Result & Answer Breakdown
```

## 📋 Examination Details

| Detail | Value |
|---|---|
| Exam Type | Multiple Choice Questions |
| Questions | 8 |
| Options per Question | 4 |
| Duration | 30 Minutes |
| Evaluation | Automatic |
| Result | Immediate |
| Interface | Desktop GUI |
| Framework | Java Swing |

## 📂 Project Structure

```text
online-Examination-system-using-java/
│
├── ExaminationSystem.java
├── README.md
└── .gitignore
```

> Compiled `.class` files are excluded from version control.

## 🚀 Getting Started

### Prerequisites

Install a JDK and verify it:

```bash
java -version
javac -version
```

### Clone

```bash
git clone https://github.com/Newtonsingh098/online-Examination-system-using-java.git
cd online-Examination-system-using-java
```

### Compile & Run

```bash
javac ExaminationSystem.java
java ExaminationSystem
```

### Optional Self-Test

```bash
java ExaminationSystem --self-test
```

## 🔑 Demo Login

```text
Username: student
Password: student123
```

> Demo credentials are for testing only. Production systems should use secure password hashing and persistent authentication.

## 📸 Screenshots

Recommended screenshots to add:

- Login screen
- Student profile screen
- Examination screen with timer
- Result screen

Example:

```markdown
![Login Screen](screenshots/login.png)
![Exam Screen](screenshots/exam.png)
![Result Screen](screenshots/result.png)
```

## 🎥 Project Demo

Add the project demonstration video here to showcase the complete examination workflow, including login, profile, exam timer, question navigation, submission, and result calculation.

## 📚 What I Learned

- Strengthened Core Java and OOP skills.
- Built a desktop GUI using Java Swing.
- Practiced event-driven programming and screen navigation.
- Implemented a real-time examination timer.
- Developed automatic scoring and result reporting.
- Improved logical thinking, problem solving, and code organization.

## 🔮 Future Improvements

-  MySQL/database integration
-  Multiple student accounts
-  Secure password hashing
-  Admin dashboard
-  Question management
-  Performance analytics
-  Leaderboard
-  PDF result generation
-  Randomized question sets
-  Web version using Spring Boot

## 🙏 Acknowledgement

This project was developed as part of my **Java Development Internship at Oasis Infobyte**. I am grateful for the opportunity to gain practical experience through hands-on Java development tasks.

## 👨‍💻 Author

**Newton Singh**  
Java Developer | Software Development Enthusiast

GitHub: https://github.com/Newtonsingh098

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐ on GitHub.

## 📄 License

This project is intended for educational and learning purposes.

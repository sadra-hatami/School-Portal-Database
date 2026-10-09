<div align="center">

# 🏫

### A SQL Server database schema for a school portal

Users and roles, courses, enrollment, exams, scores, protests, absences, messages, and news. The structure is ready to import, so the portal's data layer can be rebuilt.

# 👨‍💻 **Sadra Hatami**

### *Developer • Software Engineer • Creator*

[![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)](https://www.microsoft.com/sql-server)
[![T-SQL](https://img.shields.io/badge/T--SQL-Schema%20Scripts-003B57?style=for-the-badge)](https://learn.microsoft.com/sql/t-sql/language-reference)
[![SSMS](https://img.shields.io/badge/Run%20with-SSMS-0078D4?style=for-the-badge)](https://learn.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)
[![Tables](https://img.shields.io/badge/Tables-15-2C3E50?style=for-the-badge)](#-database-schema)
[![Versions](https://img.shields.io/badge/SQL%20Server-2008%20%7C%202012-1ABC9C?style=for-the-badge)](#-whats-inside)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](https://opensource.org/license/mit)
[![Open Source](https://img.shields.io/badge/Open_Source-Project-black?style=for-the-badge&logo=github)](https://opensource.org/)

[🌐 GitHub Profile](https://github.com/sadra-hatami) • [📧 Email](mailto:sadra.hatami.1732@gmail.com)

</div>

---

# 📑 Table of Contents

- [About](#-about)
- [Why This Project?](#-why-this-project)
- [Key Features](#-key-features)
- [What's Inside](#-whats-inside)
- [Database Schema](#-database-schema)
- [Technologies](#️-technologies)
- [Installation](#-installation)
- [Usage](#️-usage)
- [Notes](#-notes)
- [FAQ](#-faq)
- [Contact](#-contact)
- [License](#-license)
- [Support](#-support)

---

# 📖 About

**School Portal Database** is the SQL Server database behind a school portal.

It holds the structure for 15 tables: login accounts and roles, personal profiles, fields of study, a course catalog, course offerings per term, student enrollment, exams, scores, score protests, absences, private messages, news, and shared links.

This repository contains the **schema only**. There is no application code and no data.

> **Tagline:** *A SQL Server database schema for a school portal: users and roles, courses, enrollment, exams, scores, protests, absences, messages, and news.*

---

# 🚀 Why This Project?

A school portal is more than a login form. It needs people with different roles, courses that run in terms, exams that produce scores, and a way to question those scores.

This project keeps that whole picture in one place:

- Users, profiles, and roles are separate tables
- A course is defined once and offered many times
- Exams, scores, and protests are linked together
- Absences, messages, and news have their own tables
- Scripts for two SQL Server versions and a diagram are included

It is a practice database design. For a portal that uses MySQL, see [Student Portal](https://github.com/sadra-hatami/Student-Portal).

---

# ✨ Key Features

- 🔐 Accounts with hashed passwords and an active flag
- 👤 Personal profiles with national code, grade, and field
- 🎭 Roles with a many-to-many user link
- 📚 Course catalog grouped by field of study
- 🗓️ Course offerings per term, with teacher, place, and time
- 📝 Student course selection
- 🧪 Exams with date and location
- 📊 Scores with grader and record time
- ⚖️ Score protests with student and teacher explanations
- 🚫 Absence records, justified or not
- ✉️ Private messages with read status
- 📰 News with picture and author
- 🔗 Shared links
- 🧾 One-page diagram in `School.pdf`

---

# 📦 What's Inside

| File | Description |
| ---- | ----------- |
| `script_2008.sql` | Schema script generated for SQL Server 2008 |
| `script_2012.sql` | Schema script generated for SQL Server 2012 |
| `School.pdf` | One-page diagram of tables and fields |
| `README.md` | This file |

```
School-Portal-Database/
├── script_2008.sql
├── script_2012.sql
├── School.pdf
└── README.md
```

Both scripts create the same 15 tables. Pick the one that matches your server. The 2012 script also works on newer versions.

---

# 🗂️ Database Schema

### Users and roles

| Table | Purpose |
| ----- | ------- |
| `Users` | Email, hashed password, phone number, active flag, last-seen time |
| `UserDetails` | Name, family name, age, field, grade, academic orientation, national code, postal code, photo, parent's national code |
| `Roles` | Role names, such as student, teacher, or admin |
| `UserRole` | Many-to-many link between users and roles |

### Academics

| Table | Purpose |
| ----- | ------- |
| `Fields` | Fields of study |
| `Courses` | Course name, description, and its field |
| `CoursesOffered` | A course offered in a term, with teacher, class location, and schedule |
| `SelectedCourses` | Courses a student has enrolled in |
| `Exam` | Exam date, time, and location for an offered course |
| `Scores` | A student's score on an exam, with grader and record time |
| `Protest` | Score protests with student and teacher explanations and a read flag |
| `Absence` | Absence date, explanation, and whether it was justified |

### Communication

| Table | Purpose |
| ----- | ------- |
| `Messages` | Private messages with read status and time |
| `News` | News title, text, picture, author, and writing time |
| `Links` | Shared links with title, description, and address |

For every column and data type, open `School.pdf` or read the `CREATE TABLE` statements in the scripts.

---

# 🛠️ Technologies

- Microsoft SQL Server
- T-SQL
- SQL Server Management Studio (SSMS)

---

# 🚀 Installation

```bash
git clone https://github.com/sadra-hatami/School-Portal-Database.git
cd School-Portal-Database
```

1. Open SSMS and connect to your server.
2. Create an empty database named `School`:

   ```sql
   CREATE DATABASE [School];
   ```

3. Open `script_2008.sql` or `script_2012.sql`, depending on your server version.
4. Make sure the `School` database is selected. Each script starts with `USE [School]`.
5. Run the script.

---

# ▶️ Usage

After the script finishes, the 15 tables exist and are empty.

1. Add your roles to `Roles`.
2. Create accounts in `Users` and profiles in `UserDetails`.
3. Link users to roles in `UserRole`.
4. Add fields, courses, and offerings, then let students pick courses.
5. Add exams and record scores.

Connect your own application to the database to build the portal on top of it.

---

# 📝 Notes

- The `.sql` files use **UTF-16** encoding, the SSMS default. If your editor shows garbled text, reopen the file as UTF-16, or convert it:

  ```bash
  iconv -f UTF-16 -t UTF-8 script_2012.sql > script_2012_utf8.sql
  ```

- `Users.HashedPass` is meant for a **hashed** password. Never store a plain password.
- `UserDetails` holds personal data such as national codes. Do not commit real data to a public repository.
- `Messages.Id` and `Scores.Id` are not identity columns, so your application must supply their values.
- `News.Pic` and `UserDetails.Pic` use the `image` type, which Microsoft has deprecated in favor of `varbinary(max)`.
- The SQL Server backup of this database is not part of this repository.

---

# ❓ FAQ

### Does this repository contain data?

No. The scripts only create tables.

### Which script should I run?

Use `script_2008.sql` for SQL Server 2008, and `script_2012.sql` for 2012 or newer.

### Is this the same as Student Portal?

No. [Student Portal](https://github.com/sadra-hatami/Student-Portal) is a PHP application with a MySQL database. This repository is a separate SQL Server schema.

### Can I use it with MySQL or PostgreSQL?

Not directly. The scripts use T-SQL features, so they need changes first.

---

# 📬 Contact

**Developer:**

### Sadra Hatami

📧 [Email](mailto:sadra.hatami.1732@gmail.com)

🌐 [GitHub](https://github.com/sadra-hatami)

---

# 📄 License

This project is licensed under the **MIT License**.

---

# ⭐ Support

If this schema is useful as a study sample, please consider giving it a ⭐ on GitHub.

---

<div align="center">

## Designed & Developed with ❤️ for the developer community of Iran and the world by **Sadra Hatami**

</div>

# 🕌 Smart Mosque Management System

A full-stack web application for managing mosque-related activities in Bangladesh.

**Live Demo:** https://smart-mosque-management.onrender.com

**Course:** Database Management System (CSE-2423)

---

## 📋 Features

### ✅ Completed
- 🕌 **Mosque Management** — Add, search, view mosques with prayer times & Google Maps
- 📚 **Maktab Management** — Islamic schools with student enrollment & donations
- 📅 **Event (Mahfil) Locator** — Create and discover Islamic events
- ❓ **Q&A System** — Post questions and get community answers
- 🔐 **User Authentication** — JWT-based login/register/logout
- 🕐 **Prayer Times** — Daily prayer times by district (Aladhan API)
- 🌙 **Ramadan Schedule** — Sehri & Iftar times by district (Aladhan API)
- 💰 **Donation System** — Fund mosques and maktabs (anonymous supported)
- ⚙️ **Admin Dashboard** — Manage all data from frontend
- 🌓 **Dark Mode** — Toggle dark/light theme
- 📱 **Responsive Design** — Works on mobile and desktop

### 🔲 Planned
- 📖 Course/Learning Module with Payment (SSLCommerz)
- 📊 Admin Statistics Dashboard
- 🔔 Push Notifications
- 📱 Progressive Web App (PWA)

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Node.js, Express.js |
| Database | PostgreSQL |
| ORM | Prisma v7 |
| Authentication | JWT (jsonwebtoken) |
| Frontend | HTML, CSS, JavaScript |
| External API | Aladhan (Prayer Times) |
| Hosting | Render |

---

## 🗄️ Database Schema

8 main tables:
- **User** — Authentication & roles
- **Mosque** — Mosque information & prayer times
- **Maktab** — Islamic schools
- **Student** — Enrolled students
- **Funding** — Donations to mosques/maktabs
- **Event** — Mahfil & Islamic events
- **Question** — Q&A questions
- **Answer** — Q&A answers

---

## 🚀 Local Setup

```bash
git clone https://github.com/rasel3017/Smart_Mosque_Management.git
cd Smart_Mosque_Management
npm install
npx prisma migrate dev
npm run seed
npm run dev

📁 Project Structure
smart-mosque-management/
├── docs/            → ERD and Features PDF
├── public/          → Frontend (HTML, CSS, JS)
├── src/
│   ├── server.js    → Entry point
│   ├── config/      → Database connection
│   ├── controllers/ → Business logic
│   ├── routes/      → API endpoints
│   ├── middleware/  → Auth middleware
│   └── validation/  → Input validation
├── prisma/
│   ├── schema.prisma → Database models
│   └── seed.js       → Sample data
└── package.json
📄 Some API Endpoints
Module
Method
Endpoint
Auth
POST
/api/auth/register
Auth
POST
/api/auth/login
Mosque
GET
/api/mosques/all
Mosque
GET
/api/mosques/region/:region
Maktab
GET
/api/maktabs
Events
GET
/api/events
Q&A
GET
/api/qa/questions
Prayer
External
Aladhan API

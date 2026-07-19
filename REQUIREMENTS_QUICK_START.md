# Web App Recruitment Test - Quick Start Guide

## 🎯 Overview
This recruitment test evaluates your web development skills by having you build a complete web application. Choose a project that matches your experience level and complete it within the suggested timeframe.

## 📋 Choose Your Project Level

### 🟢 Beginner (4-8 hours)
- **Todo App**: CRUD operations, local storage, filtering
- **Weather App**: API integration, search, data display
- **Recipe Finder**: API search, favorites, responsive design

### 🟡 Intermediate (8-16 hours)
- **Blog Platform**: Auth, CRUD posts, comments, categories
- **E-commerce Catalog**: Product listing, filters, cart, search
- **Task Dashboard**: Projects, drag-and-drop, due dates

### 🔴 Advanced (16-24 hours)
- **Social Media**: Profiles, posts, likes, comments, real-time
- **Project Management**: Workspaces, Kanban, assignments, time tracking
- **Booking System**: Calendar, availability, payments, notifications

## 🛠️ Technology Stack

### Frontend (Choose one)
- React + TypeScript (Recommended)
- Vue + TypeScript
- Angular + TypeScript
- Svelte

### Backend (Choose one, if needed)
- Node.js (Express/NestJS)
- Python (Django/Flask/FastAPI)
- Ruby on Rails
- Java (Spring Boot)
- C# (.NET Core)

### Database (Choose one, if needed)
- PostgreSQL / MySQL
- MongoDB
- Firebase

## 📦 Submission Checklist

- [ ] Complete source code in Git repository
- [ ] Comprehensive README.md with:
  - Project description
  - Features implemented
  - Tech stack
  - Setup instructions
  - Running instructions
  - Testing instructions
- [ ] Live demo URL (optional but encouraged)
- [ ] Screenshots of the application
- [ ] No sensitive data in repository
- [ ] Proper .gitignore file

## ⚡ Quick Setup Template

```bash
# Create your project
npx create-react-app my-recruitment-test --template typescript
cd my-recruitment-test

# Or for Vite
npm create vite@latest my-recruitment-test -- --template react-ts
cd my-recruitment-test

# Initialize git
git init
git add .
git commit -m "Initial project setup"

# Create a new branch
git checkout -b recruitment-test
```

## 📊 Evaluation Criteria

| Criteria | Weight | What We Look For |
|----------|--------|------------------|
| Code Quality | 40% | Clean, readable, maintainable code |
| Functionality | 30% | Features work, edge cases handled |
| Architecture | 20% | Good structure, separation of concerns |
| Documentation | 10% | Clear README, good comments |

## 🎯 Pro Tips

1. **Start Simple**: Begin with core features, then add extras
2. **Commit Often**: Small, frequent commits with good messages
3. **Test As You Go**: Don't leave testing to the end
4. **Document Early**: Write your README as you build
5. **Focus on Quality**: Better to have fewer features done well

## 📚 Recommended Free APIs

- [JSONPlaceholder](https://jsonplaceholder.typicode.com/) - Fake REST API
- [OpenWeatherMap](https://openweathermap.org/api) - Weather data
- [TheMovieDB](https://www.themoviedb.org/documentation/api) - Movies
- [GitHub API](https://docs.github.com/en/rest) - Repos

## 🚀 Deployment Options (Free Tier)

- **Frontend**: Vercel, Netlify, GitHub Pages
- **Backend**: Render, Railway, Cyclic
- **Full-stack**: Vercel, Netlify

## ❓ Need Help?

Check the full [REQUIREMENTS.md](./REQUIREMENTS.md) for detailed information on:
- Functional requirements
- Non-functional requirements
- Project suggestions
- Evaluation details
- Best practices

---

**Good luck! Show us your best work.** 💪

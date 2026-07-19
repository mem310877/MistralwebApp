# Web App Recruitment Test - Requirements Document

## 1. Introduction

### 1.1 Purpose
This document outlines the requirements for a web application recruitment test designed to evaluate candidates' technical skills in web development, including frontend, backend, and full-stack capabilities.

### 1.2 Scope
The recruitment test will assess candidates' ability to:
- Build a functional web application
- Implement clean, maintainable code
- Follow best practices in web development
- Solve real-world problems
- Work with modern web technologies

### 1.3 Target Audience
- Recruitment team
- Technical interviewers
- Development candidates

---

## 2. Overall Description

### 2.1 System Overview
The web application should demonstrate the candidate's ability to create a complete, functional web solution with the following characteristics:
- Responsive user interface
- RESTful API or backend logic
- Data persistence
- User authentication (optional, based on complexity)
- Error handling and validation

### 2.2 Technology Stack Requirements
Candidates should use modern web technologies. Suggested stacks include:

**Frontend:**
- React.js / Vue.js / Angular / Svelte
- TypeScript (preferred) or JavaScript
- CSS preprocessors (Sass, Less) or CSS-in-JS
- Responsive design frameworks (Bootstrap, Tailwind, Material-UI)

**Backend (if applicable):**
- Node.js (Express, NestJS)
- Python (Django, Flask, FastAPI)
- Ruby on Rails
- Java (Spring Boot)
- C# (.NET Core)
- Go

**Database:**
- SQL (PostgreSQL, MySQL)
- NoSQL (MongoDB, Firebase)
- ORM/ODM libraries

### 2.3 Project Structure
```
project-root/
├── client/           # Frontend application
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── styles/
│   │   ├── utils/
│   │   ├── App.jsx/tsx
│   │   └── index.jsx/tsx
│   └── package.json
├── server/           # Backend application (if applicable)
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── config/
│   └── package.json
├── README.md         # Project documentation
├── .gitignore
└── package.json      # Root package.json (if monorepo)
```

---

## 3. Functional Requirements

### 3.1 Core Features

#### FR-001: User Interface
- **Description**: The application must have a responsive, intuitive user interface
- **Priority**: High
- **Acceptance Criteria**:
  - Works on desktop, tablet, and mobile devices
  - Clean, modern design
  - Intuitive navigation
  - Accessible (WCAG 2.1 AA minimum)

#### FR-002: Data Display
- **Description**: The application must display data from an API or data source
- **Priority**: High
- **Acceptance Criteria**:
  - Data is fetched and displayed correctly
  - Loading states are implemented
  - Error states are handled gracefully
  - Data can be filtered/sorted (if applicable)

#### FR-003: Data Manipulation
- **Description**: The application must allow users to create, read, update, and delete data (CRUD operations)
- **Priority**: High
- **Acceptance Criteria**:
  - Users can add new items
  - Users can view existing items
  - Users can edit existing items
  - Users can delete items
  - Changes persist between sessions

#### FR-004: Form Handling
- **Description**: The application must include at least one form with validation
- **Priority**: Medium
- **Acceptance Criteria**:
  - Form fields are validated
  - Error messages are clear and helpful
  - Form submission works correctly
  - Success feedback is provided

### 3.2 Optional Features (Bonus Points)

#### FR-005: User Authentication
- **Description**: Implement user registration and login
- **Priority**: Low
- **Acceptance Criteria**:
  - Users can register with email/password
  - Users can login/logout
  - Protected routes are accessible only to authenticated users
  - JWT or session-based authentication

#### FR-006: Search Functionality
- **Description**: Implement search across application data
- **Priority**: Low
- **Acceptance Criteria**:
  - Search works in real-time or on submit
  - Results are relevant
  - Empty state is handled

#### FR-007: Pagination
- **Description**: Implement pagination for large datasets
- **Priority**: Low
- **Acceptance Criteria**:
  - Data is split across pages
  - Navigation between pages works
  - Page size can be changed (optional)

#### FR-008: Real-time Updates
- **Description**: Implement WebSocket or polling for real-time features
- **Priority**: Low
- **Acceptance Criteria**:
  - Changes are reflected without page refresh
  - Connection errors are handled

---

## 4. Non-Functional Requirements

### 4.1 Performance
- **NFR-001**: The application must load within 2 seconds on a standard broadband connection
- **NFR-002**: API responses must be under 500ms for 95% of requests
- **NFR-003**: The application must handle at least 100 concurrent users

### 4.2 Security
- **NFR-004**: All user inputs must be sanitized to prevent XSS attacks
- **NFR-005**: Authentication tokens must be stored securely (HttpOnly, Secure cookies)
- **NFR-006**: Sensitive data must be encrypted in transit (HTTPS)
- **NFR-007**: Passwords must be hashed using bcrypt or similar

### 4.3 Code Quality
- **NFR-008**: Code must follow consistent style guidelines (ESLint, Prettier)
- **NFR-009**: Code must be modular and reusable
- **NFR-010**: Functions/components must be well-documented
- **NFR-011**: No sensitive information (API keys, passwords) in code
- **NFR-012**: Proper error handling at all levels

### 4.4 Testing
- **NFR-013**: Unit tests for critical business logic
- **NFR-014**: Integration tests for API endpoints
- **NFR-015**: End-to-end tests for user flows (optional but encouraged)
- **NFR-016**: Test coverage should be at least 70%

### 4.5 Accessibility
- **NFR-017**: All interactive elements must be keyboard navigable
- **NFR-018**: Color contrast must meet WCAG 2.1 AA standards
- **NFR-019**: ARIA labels must be used where appropriate
- **NFR-020**: Screen reader compatibility

### 4.6 SEO (if applicable)
- **NFR-021**: Proper meta tags for important pages
- **NFR-022**: Semantic HTML structure
- **NFR-023**: Sitemap generation (for multi-page apps)

---

## 5. Technical Requirements

### 5.1 Frontend Requirements
- Use a modern frontend framework (React, Vue, Angular, Svelte)
- Implement state management (Context API, Redux, Zustand, Pinia, etc.)
- Use TypeScript (strongly recommended)
- Responsive design using media queries or a CSS framework
- Component-based architecture
- Proper separation of concerns

### 5.2 Backend Requirements (if applicable)
- RESTful API design
- Proper HTTP status codes
- Input validation
- Rate limiting (optional)
- CORS configuration
- Environment variables for configuration

### 5.3 Database Requirements (if applicable)
- Proper schema design
- Indexes for performance-critical queries
- Relationships between entities
- Data validation at the database level
- Backup and restore procedures (documented)

### 5.4 DevOps Requirements
- Docker containerization (optional but encouraged)
- Clear setup instructions in README
- Environment configuration
- Build and deployment scripts

---

## 6. Project Suggestions

### 6.1 Beginner Level (4-8 hours)
1. **Todo Application**
   - Create, read, update, delete tasks
   - Filter tasks by status (completed, active)
   - Local storage for persistence

2. **Weather App**
   - Fetch weather data from a public API (OpenWeatherMap, etc.)
   - Display current weather and forecast
   - Search by location

3. **Recipe Finder**
   - Search recipes from an API (Edamam, Spoonacular)
   - Display recipe details
   - Save favorite recipes

### 6.2 Intermediate Level (8-16 hours)
1. **Blog Platform**
   - User authentication
   - Create, edit, delete blog posts
   - Comment system
   - Categories and tags

2. **E-commerce Product Catalog**
   - Product listing with filters
   - Product details page
   - Shopping cart functionality
   - Search functionality

3. **Task Management Dashboard**
   - Multiple projects/boards
   - Drag-and-drop task organization
   - Due dates and priorities
   - Team collaboration features

### 6.3 Advanced Level (16-24 hours)
1. **Social Media Platform**
   - User profiles
   - Posts with likes and comments
   - Friend/follow system
   - Real-time notifications

2. **Project Management Tool**
   - Multiple workspaces
   - Kanban boards
   - Task assignments
   - Time tracking
   - File attachments

3. **Booking System**
   - Calendar integration
   - Availability management
   - Payment processing (mock)
   - Email notifications

---

## 7. Evaluation Criteria

### 7.1 Code Quality (40%)
- [ ] Clean, readable code
- [ ] Consistent naming conventions
- [ ] Proper error handling
- [ ] No code duplication (DRY principle)
- [ ] Appropriate use of design patterns
- [ ] Meaningful commit messages

### 7.2 Functionality (30%)
- [ ] All required features implemented
- [ ] Features work as expected
- [ ] Edge cases handled
- [ ] No critical bugs
- [ ] Performance meets requirements

### 7.3 Architecture & Design (20%)
- [ ] Logical project structure
- [ ] Separation of concerns
- [ ] Scalable architecture
- [ ] Proper use of frameworks/libraries
- [ ] API design (if applicable)

### 7.4 Documentation (10%)
- [ ] Clear README with setup instructions
- [ ] Code comments where necessary
- [ ] API documentation (if applicable)
- [ ] Explanation of design decisions

---

## 8. Submission Requirements

### 8.1 Deliverables
1. **Source Code**: Complete project code in a Git repository
2. **README.md**: Comprehensive documentation including:
   - Project description
   - Features implemented
   - Technology stack
   - Setup instructions
   - Running the application
   - Testing instructions
   - Deployment notes (if applicable)
3. **Live Demo** (optional but encouraged): Deployed application URL
4. **Screenshots**: Visual documentation of the application

### 8.2 Git Best Practices
- Regular, meaningful commits
- Proper branch naming
- Pull requests for major features (if working in a team)
- .gitignore file
- No sensitive data in repository

### 8.3 Submission Format
```
recruitment-test-submission/
├── project/              # Your project code
│   ├── client/
│   ├── server/
│   └── README.md
├── SCREENSHOTS.md       # Screenshots of your application
└── SUBMISSION_NOTES.md  # Any additional notes
```

---

## 9. Timeline

| Phase | Duration | Description |
|-------|----------|-------------|
| Planning | 1 hour | Understand requirements, choose project |
| Setup | 1 hour | Initialize project, set up environment |
| Development | Varies | Implement features based on chosen project |
| Testing | 2 hours | Test all features, fix bugs |
| Documentation | 1 hour | Write README, add comments |
| Review | 1 hour | Final review, clean up code |

---

## 10. Resources

### 10.1 Recommended APIs
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/) - Fake REST API
- [OpenWeatherMap](https://openweathermap.org/api) - Weather data
- [Edamam Recipe API](https://developer.edamam.com/) - Recipe data
- [TheMovieDB](https://www.themoviedb.org/documentation/api) - Movie data
- [GitHub API](https://docs.github.com/en/rest) - Repository data

### 10.2 Learning Resources
- [MDN Web Docs](https://developer.mozilla.org/) - Web development reference
- [React Documentation](https://react.dev/) - React framework
- [Vue Documentation](https://vuejs.org/) - Vue framework
- [Express Documentation](https://expressjs.com/) - Node.js backend
- [Django Documentation](https://docs.djangoproject.com/) - Python backend

### 10.3 Tools
- [Git](https://git-scm.com/) - Version control
- [GitHub](https://github.com/) - Code hosting
- [Vercel](https://vercel.com/) - Frontend deployment
- [Render](https://render.com/) - Backend deployment
- [Netlify](https://www.netlify.com/) - Full-stack deployment

---

## 11. FAQ

### Q: Can I use any technology I want?
A: Yes, as long as it's a modern web technology. We recommend using technologies you're comfortable with to showcase your best work.

### Q: Do I need to implement all features?
A: Focus on implementing the core features well. Optional features are bonus points but not required.

### Q: Can I use templates or starter kits?
A: You can use minimal starter templates (like Create React App, Vite), but the majority of the code should be your own work.

### Q: How detailed should my documentation be?
A: Your README should be comprehensive enough that someone else could run your project without asking you questions.

### Q: What if I don't finish in the suggested time?
A: Submit what you have. A partially completed but well-implemented project is better than a rushed, buggy one.

### Q: Can I work in a team?
A: This test is designed for individual assessment. All work should be your own.

---

## 12. Appendix

### A. Sample Project: Todo Application

**Requirements:**
1. Display a list of todos
2. Add new todos
3. Mark todos as complete
4. Delete todos
5. Filter todos (all, active, completed)
6. Persist todos in localStorage

**Evaluation Focus:**
- State management
- Component structure
- Event handling
- Local storage usage
- Responsive design

### B. Sample Project: Weather App

**Requirements:**
1. Search for a city
2. Display current weather
3. Display 5-day forecast
4. Show weather icons
5. Handle API errors
6. Persist last searched city

**Evaluation Focus:**
- API integration
- Error handling
- Data transformation
- UI/UX design
- Responsive layout

### C. Sample Project: Blog Platform

**Requirements:**
1. User registration and login
2. Create, edit, delete blog posts
3. View all posts
4. View single post with comments
5. Add comments to posts
6. User profiles

**Evaluation Focus:**
- Authentication flow
- Database design
- API design
- State management
- Form validation
- Security considerations

---

*Document Version: 1.0*
*Last Updated: 2024*
*Author: Vibe Code (Mistral AI)*

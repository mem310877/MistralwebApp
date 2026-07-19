# [34mWeb Application Recruitment Test - Design Plan[0m
## [1mMistral AI Technical Assessment Framework[0m

---

## [32m[1m1. EXECUTIVE SUMMARY[0m

### 1.1 Assessment Overview
This design plan outlines the technical architecture, implementation strategy, and evaluation framework for the Mistral AI Web Application Recruitment Test. It serves as a comprehensive guide for both candidates (to understand expectations) and evaluators (to assess submissions consistently).

### 1.2 Design Philosophy
- **Progressive Complexity**: Projects scale from beginner to advanced to accommodate various experience levels
- **Technology Agnostic**: Candidates can showcase skills in their preferred modern web stack
- **Real-World Focus**: Requirements mirror actual production scenarios
- **Quality Over Quantity**: Emphasis on clean code, architecture, and best practices

### 1.3 Target Outcomes
| Outcome | Beginner | Intermediate | Advanced |
|---------|----------|--------------|----------|
| **Time Investment** | 4-8 hours | 8-16 hours | 16-24 hours |
| **Complexity** | Single-page, client-side | Full-stack, basic auth | Full-stack, real-time |
| **Evaluation Depth** | UI/State Management | Architecture/API Design | System Design/Scale |

---

## [32m[1m2. ARCHITECTURE OVERVIEW[0m

### 2.1 System Architecture Patterns

#### [33mOption A: Client-Side Only (Beginner)[0m
```
┌─────────────────────────────────────────────────────────────┐
│                        User Browser                            │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────────┐  │
│  │   Frontend  │◄──►│   Local     │    │   External API   │  │
│  │  Framework   │    │   Storage    │    │   (Optional)     │  │
│  └─────────────┘    └─────────────┘    └─────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```
**Use Case**: Todo App, Weather App, Recipe Finder
**Tech Stack**: React/Vue + TypeScript + LocalStorage

#### [33mOption B: Client-Server (Intermediate)[0m
```
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────┐
│      Client          │     │       Server         │     │     Database     │
│  ┌───────────────┐  │◄──►│  ┌───────────────┐  │◄──►│  ┌───────────┐  │
│  │  Frontend      │  │     │  │  Backend       │  │     │  │  SQL/NoSQL │  │
│  │  Framework     │  │     │  │  Framework     │  │     │  └───────────┘  │
│  └───────────────┘  │     │  └───────────────┘  │     └─────────────────┘
└─────────────────────┘     └─────────────────────┘
```
**Use Case**: Blog Platform, E-commerce Catalog
**Tech Stack**: React + Node.js/Express + PostgreSQL

#### [33mOption C: Full-Stack with Real-Time (Advanced)[0m
```
┌─────────────────────┐     ┌─────────────────────────────────┐     ┌─────────────────┐
│      Client          │     │           Server Layer            │     │     Database     │
│  ┌───────────────┐  │◄──►│  ┌─────────────┐  ┌─────────────┐  │◄──►│  ┌───────────┐  │
│  │  Frontend      │  │     │  │  REST API   │  │  WebSocket   │  │     │  │  SQL/NoSQL │  │
│  │  Framework     │  │     │  │             │  │  Server      │  │     │  └───────────┘  │
│  └───────────────┘  │     │  └─────────────┘  └─────────────┘  │     └─────────────────┘
└─────────────────────┘     └─────────────────────────────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │   Message Queue      │
                    │   (Redis, RabbitMQ)  │
                    └─────────────────────┘
```
**Use Case**: Social Media Platform, Project Management Tool
**Tech Stack**: React + Node.js + PostgreSQL + Socket.io + Redis

---

## [32m[1m3. TECHNICAL SPECIFICATIONS[0m

### 3.1 Frontend Architecture

#### [36mComponent Hierarchy (React Example)[0m
```
App
├── providers/
│   ├── ThemeProvider
│   ├── AuthProvider
│   └── DataProvider
├── components/
│   ├── common/
│   │   ├── Button
│   │   ├── Input
│   │   ├── Modal
│   │   └── Card
│   ├── layout/
│   │   ├── Header
│   │   ├── Footer
│   │   ├── Sidebar
│   │   └── Layout
│   └── features/
│       ├── TodoList
│       ├── TodoItem
│       ├── TodoForm
│       └── TodoFilter
├── pages/
│   ├── Home
│   ├── Dashboard
│   ├── Login
│   └── NotFound
├── hooks/
│   ├── useTodos
│   ├── useAuth
│   └── useLocalStorage
├── services/
│   ├── api
│   ├── auth
│   └── storage
├── utils/
│   ├── validators
│   ├── formatters
│   └── helpers
└── styles/
    ├── globals.css
    ├── theme.css
    └── components.css
```

#### [36mState Management Strategy[0m

| Project Level | Recommended Approach | Complexity | Use Case |
|---------------|----------------------|------------|----------|
| Beginner | React Context + useReducer | Low | Todo App |
| Beginner | Zustand | Low | Weather App |
| Intermediate | Redux Toolkit | Medium | Blog Platform |
| Intermediate | React Query | Medium | E-commerce |
| Advanced | Redux Toolkit + RTK Query | High | Social Media |
| Advanced | Zustand + Immer | High | Project Management |

#### [36mStyling Approach[0m

| Approach | Pros | Cons | Best For |
|----------|------|------|----------|
| **CSS Modules** | Scoped styles, no conflicts | Manual theming | Beginner Projects |
| **Tailwind CSS** | Rapid development, utility-first | Learning curve | All Levels |
| **Styled Components** | CSS-in-JS, dynamic styles | Runtime overhead | Component Libraries |
| **Material-UI** | Pre-built components, consistent | Bundle size | Admin Dashboards |
| **Chakra UI** | Accessible, themeable | Less customizable | Rapid Prototyping |

### 3.2 Backend Architecture

#### [36mAPI Design Principles[0m

**RESTful Endpoints (Standard):**
```
GET    /api/todos          -> List all todos
POST   /api/todos          -> Create new todo
GET    /api/todos/:id      -> Get single todo
PUT    /api/todos/:id      -> Update todo
DELETE /api/todos/:id      -> Delete todo
PATCH  /api/todos/:id      -> Partial update
```

**GraphQL Alternative (Advanced):**
```graphql
# Query
query GetTodos {
  todos(where: { completed: false }) {
    id
    title
    completed
    createdAt
  }
}

# Mutation
mutation CreateTodo($input: TodoInput!) {
  createTodo(input: $input) {
    id
    title
    completed
  }
}
```

#### [36mLayered Architecture[0m
```
┌─────────────────────────────────────────────────────────────┐
│                        API Layer                               │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────────┐  │
│  │  Controllers │◄──►│   Services   │◄──►│   Repositories   │  │
│  └─────────────┘    └─────────────┘    └─────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │     Database         │
                    └─────────────────────┘
```

**Controller (Route Handler):**
- Validates request
- Calls appropriate service
- Returns HTTP response

**Service (Business Logic):**
- Contains core business logic
- Orchestrates multiple operations
- Handles transactions

**Repository (Data Access):**
- Direct database interaction
- CRUD operations
- Query building

### 3.3 Database Design

#### [36mRelational Database (PostgreSQL Example)[0m

**Blog Platform Schema:**
```sql
-- Users table
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    name VARCHAR(100),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- Posts table
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    status VARCHAR(20) DEFAULT 'draft' CHECK (status IN ('draft', 'published', 'archived')),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- Comments table
CREATE TABLE comments (
    id SERIAL PRIMARY KEY,
    post_id INTEGER REFERENCES posts(id) ON DELETE CASCADE,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

-- Categories table (Many-to-Many with Posts)
CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE post_categories (
    post_id INTEGER REFERENCES posts(id) ON DELETE CASCADE,
    category_id INTEGER REFERENCES categories(id) ON DELETE CASCADE,
    PRIMARY KEY (post_id, category_id)
);

-- Indexes for performance
CREATE INDEX idx_posts_user_id ON posts(user_id);
CREATE INDEX idx_posts_status ON posts(status);
CREATE INDEX idx_comments_post_id ON comments(post_id);
```

#### [36mNoSQL Database (MongoDB Example)[0m

**E-commerce Product Schema:**
```javascript
// Product Document
{
  _id: ObjectId,
  sku: String, // Unique identifier
  name: { type: String, required: true },
  description: String,
  price: { type: Number, required: true, min: 0 },
  compareAtPrice: Number,
  cost: Number,
  categories: [{ type: String, index: true }],
  tags: [String],
  images: [{
    url: String,
    altText: String,
    isPrimary: Boolean
  }],
  inventory: {
    quantity: { type: Number, default: 0 },
    inStock: { type: Boolean, default: true },
    trackQuantity: { type: Boolean, default: true }
  },
  status: {
    type: String,
    enum: ['draft', 'published', 'archived'],
    default: 'draft'
  },
  seo: {
    title: String,
    description: String,
    slug: { type: String, unique: true }
  },
  createdAt: { type: Date, default: Date.now },
  updatedAt: { type: Date, default: Date.now }
}

// Indexes
db.products.createIndex({ sku: 1 }, { unique: true });
db.products.createIndex({ name: "text", description: "text" });
db.products.createIndex({ categories: 1 });
db.products.createIndex({ status: 1 });
```

---

## [32m[1m4. IMPLEMENTATION ROADMAP[0m

### 4.1 Phase-Based Development

#### [33mPhase 1: Planning & Setup (1 hour)[0m
- [ ] Review requirements and choose project
- [ ] Select technology stack
- [ ] Create project structure
- [ ] Set up version control (Git)
- [ ] Initialize project with chosen framework
- [ ] Configure TypeScript (if using)
- [ ] Set up ESLint and Prettier
- [ ] Create basic folder structure

**Deliverables:**
- Project repository initialized
- Basic configuration files (.eslintrc, .prettierrc, tsconfig.json)
- README.md skeleton

#### [33mPhase 2: Core Features (Varies by Project)[0m

**Beginner Project (Todo App) - 3-5 hours:**
- [ ] Set up React/Vue project
- [ ] Create Todo interface/type
- [ ] Implement TodoList component
- [ ] Implement TodoItem component
- [ ] Implement TodoForm component
- [ ] Implement addTodo functionality
- [ ] Implement deleteTodo functionality
- [ ] Implement toggleTodo functionality
- [ ] Implement filter functionality (all/active/completed)
- [ ] Implement localStorage persistence
- [ ] Add basic styling

**Intermediate Project (Blog Platform) - 6-10 hours:**
- [ ] Set up full-stack project (frontend + backend)
- [ ] Create User model and authentication
- [ ] Create Post model and CRUD operations
- [ ] Create Comment model and functionality
- [ ] Implement user registration/login
- [ ] Implement protected routes
- [ ] Create post listing page
- [ ] Create single post page
- [ ] Implement comment system
- [ ] Add basic styling

**Advanced Project (Social Media) - 12-18 hours:**
- [ ] Set up full-stack project with real-time capabilities
- [ ] Create User model with profiles
- [ ] Create Post model with likes/comments
- [ ] Create Friend/Follow system
- [ ] Implement JWT authentication
- [ ] Implement post creation/editing
- [ ] Implement like functionality
- [ ] Implement comment functionality
- [ ] Implement real-time notifications (WebSocket)
- [ ] Create user profiles
- [ ] Create news feed
- [ ] Add comprehensive styling

#### [33mPhase 3: Polish & Enhancements (2-4 hours)[0m
- [ ] Add form validation
- [ ] Implement error handling
- [ ] Add loading states
- [ ] Implement empty states
- [ ] Add animations/transitions
- [ ] Improve accessibility
- [ ] Optimize performance
- [ ] Add responsive design refinements
- [ ] Implement optional features (search, pagination, etc.)

#### [33mPhase 4: Testing (2 hours)[0m
- [ ] Write unit tests for utility functions
- [ ] Write unit tests for components
- [ ] Write integration tests for API endpoints
- [ ] Test user flows manually
- [ ] Test edge cases
- [ ] Test responsive behavior
- [ ] Test cross-browser compatibility
- [ ] Achieve minimum 70% test coverage

#### [33mPhase 5: Documentation (1 hour)[0m
- [ ] Complete README.md
- [ ] Add project description
- [ ] List features implemented
- [ ] Document technology stack
- [ ] Write setup instructions
- [ ] Write running instructions
- [ ] Write testing instructions
- [ ] Add deployment notes
- [ ] Add screenshots
- [ ] Document design decisions

---

## [32m[1m5. DETAILED TECHNICAL GUIDELINES[0m

### 5.1 Frontend Best Practices

#### [36mComponent Design Principles[0m

**Single Responsibility Principle:**
```typescript
// ❌ BAD: Component does too much
const TodoList = () => {
  const [todos, setTodos] = useState<Todo[]>([]);
  const [filter, setFilter] = useState('all');
  const [newTodo, setNewTodo] = useState('');
  
  // Handles fetching, filtering, adding, deleting
  // ... 50+ lines of logic
  
  return (
    <div>
      {/* Rendering logic */}
    </div>
  );
};

// ✅ GOOD: Separated concerns
const TodoList = () => {
  const { todos, addTodo, deleteTodo, toggleTodo } = useTodos();
  const { filter, setFilter } = useFilter();
  
  return (
    <div>
      <TodoForm onAdd={addTodo} />
      <TodoFilter value={filter} onChange={setFilter} />
      <TodoItems 
        todos={todos} 
        onDelete={deleteTodo} 
        onToggle={toggleTodo}
      />
    </div>
  );
};
```

#### [36mTypeScript Best Practices[0m

**Type Definitions:**
```typescript
// ✅ GOOD: Comprehensive types
interface User {
  id: string;
  email: string;
  name: string;
  role: 'admin' | 'user' | 'guest';
  createdAt: Date;
  updatedAt: Date;
}

interface Post {
  id: string;
  user: User;
  title: string;
  content: string;
  status: 'draft' | 'published' | 'archived';
  tags: string[];
  createdAt: Date;
}

// ✅ GOOD: Generic API response type
type ApiResponse<T> = {
  success: boolean;
  data?: T;
  error?: string;
  message?: string;
};

// ✅ GOOD: Function types
 type FetchPostsFunction = (params: {
   page?: number;
   limit?: number;
   status?: Post['status'];
 }) => Promise<ApiResponse<Post[]>>;
```

**React with TypeScript:**
```typescript
// ✅ GOOD: Typed props
interface TodoItemProps {
  todo: Todo;
  onToggle: (id: string) => void;
  onDelete: (id: string) => void;
}

const TodoItem: React.FC<TodoItemProps> = ({ todo, onToggle, onDelete }) => {
  // Implementation
};

// ✅ GOOD: Typed hooks
const useTodos = (): {
  todos: Todo[];
  addTodo: (text: string) => void;
  deleteTodo: (id: string) => void;
  toggleTodo: (id: string) => void;
} => {
  // Implementation
};
```

#### [36mState Management Patterns[0m

**React Context + useReducer (Beginner):**
```typescript
// Context definition
type TodoState = {
  todos: Todo[];
  filter: 'all' | 'active' | 'completed';
};

type TodoAction = 
  | { type: 'ADD_TODO'; payload: string }
  | { type: 'TOGGLE_TODO'; payload: string }
  | { type: 'DELETE_TODO'; payload: string }
  | { type: 'SET_FILTER'; payload: 'all' | 'active' | 'completed' };

const todoReducer = (state: TodoState, action: TodoAction): TodoState => {
  switch (action.type) {
    case 'ADD_TODO':
      return { ...state, todos: [...state.todos, newTodo] };
    case 'TOGGLE_TODO':
      return { 
        ...state, 
        todos: state.todos.map(t => 
          t.id === action.payload ? { ...t, completed: !t.completed } : t
        ) 
      };
    // ... other cases
    default:
      return state;
  }
};

// Context provider
const TodoProvider: React.FC<{ children: ReactNode }> = ({ children }) => {
  const [state, dispatch] = useReducer(todoReducer, initialState);
  return (
    <TodoContext.Provider value={{ state, dispatch }}>
      {children}
    </TodoContext.Provider>
  );
};
```

**React Query (Intermediate):**
```typescript
// Custom hook for todos
const useTodos = () => {
  const queryClient = useQueryClient();
  
  // Fetch todos
  const { data: todos, isLoading, error } = useQuery<Todo[]>(
    'todos',
    fetchTodos,
    { staleTime: 5000 }
  );
  
  // Add todo mutation
  const addTodoMutation = useMutation(
    (text: string) => api.addTodo(text),
    {
      onSuccess: () => {
        queryClient.invalidateQueries('todos');
      },
    }
  );
  
  // Delete todo mutation
  const deleteTodoMutation = useMutation(
    (id: string) => api.deleteTodo(id),
    {
      onSuccess: () => {
        queryClient.invalidateQueries('todos');
      },
    }
  );
  
  return { todos, isLoading, error, addTodoMutation, deleteTodoMutation };
};
```

### 5.2 Backend Best Practices

#### [36mExpress.js API Structure[0m

```
project/
├── src/
│   ├── config/
│   │   ├── database.ts
│   │   ├── env.ts
│   │   └── cors.ts
│   ├── controllers/
│   │   ├── todo.controller.ts
│   │   ├── user.controller.ts
│   │   └── auth.controller.ts
│   ├── middlewares/
│   │   ├── auth.middleware.ts
│   │   ├── error.middleware.ts
│   │   └── validation.middleware.ts
│   ├── models/
│   │   ├── todo.model.ts
│   │   ├── user.model.ts
│   │   └── index.ts
│   ├── routes/
│   │   ├── todo.routes.ts
│   │   ├── user.routes.ts
│   │   ├── auth.routes.ts
│   │   └── index.ts
│   ├── services/
│   │   ├── todo.service.ts
│   │   ├── user.service.ts
│   │   └── auth.service.ts
│   ├── utils/
│   │   ├── logger.ts
│   │   ├── response.ts
│   │   └── validators.ts
│   ├── app.ts
│   └── server.ts
├── tests/
│   ├── unit/
│   └── integration/
├── .env
└── package.json
```

**Controller Example:**
```typescript
// todo.controller.ts
import { Request, Response, NextFunction } from 'express';
import * as todoService from '../services/todo.service';
import { TodoInput } from '../types';

export const getAllTodos = async (req: Request, res: Response, next: NextFunction) => {
  try {
    const { filter } = req.query;
    const todos = await todoService.getAllTodos(filter as string);
    res.json({
      success: true,
      data: todos,
      message: 'Todos retrieved successfully'
    });
  } catch (error) {
    next(error);
  }
};

export const createTodo = async (req: Request, res: Response, next: NextFunction) => {
  try {
    const input: TodoInput = req.body;
    const todo = await todoService.createTodo(input);
    res.status(201).json({
      success: true,
      data: todo,
      message: 'Todo created successfully'
    });
  } catch (error) {
    next(error);
  }
};
```

**Service Example:**
```typescript
// todo.service.ts
import Todo from '../models/todo.model';
import { TodoInput } from '../types';

export const getAllTodos = async (filter?: string) => {
  let query = Todo.find();
  
  if (filter === 'active') {
    query = query.where({ completed: false });
  } else if (filter === 'completed') {
    query = query.where({ completed: true });
  }
  
  return query.sort({ createdAt: -1 });
};

export const createTodo = async (input: TodoInput) => {
  const todo = new Todo({
    ...input,
    completed: false
  });
  
  await todo.save();
  return todo;
};
```

#### [36mError Handling Middleware[0m

```typescript
// error.middleware.ts
import { Request, Response, NextFunction } from 'express';

export interface AppError extends Error {
  statusCode?: number;
  errors?: { field: string; message: string }[];
}

export const errorHandler = (
  err: AppError,
  req: Request,
  res: Response,
  next: NextFunction
) => {
  // Log error
  console.error(`[${new Date().toISOString()}] Error:`, err.message);
  
  // Handle validation errors
  if (err.name === 'ValidationError') {
    return res.status(400).json({
      success: false,
      error: 'Validation Error',
      errors: Object.values(err.errors).map((e: any) => ({
        field: e.path,
        message: e.message
      }))
    });
  }
  
  // Handle duplicate key errors
  if (err.code === 11000) {
    return res.status(409).json({
      success: false,
      error: 'Duplicate Key Error',
      message: 'Resource already exists'
    });
  }
  
  // Handle JWT errors
  if (err.name === 'JsonWebTokenError') {
    return res.status(401).json({
      success: false,
      error: 'Unauthorized',
      message: 'Invalid token'
    });
  }
  
  // Default error
  const statusCode = err.statusCode || 500;
  const message = err.message || 'Internal Server Error';
  
  res.status(statusCode).json({
    success: false,
    error: message,
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
  });
};
```

### 5.3 Database Best Practices

#### [36mMongoose Models (MongoDB)[0m

```typescript
// user.model.ts
import mongoose, { Document, Schema } from 'mongoose';
import bcrypt from 'bcryptjs';

export interface IUser extends Document {
  email: string;
  password: string;
  name: string;
  role: 'admin' | 'user' | 'guest';
  comparePassword(candidatePassword: string): Promise<boolean>;
}

const UserSchema = new Schema<IUser>(
  {
    email: {
      type: String,
      required: [true, 'Email is required'],
      unique: true,
      trim: true,
      lowercase: true,
      match: [/^\S+@\S+\.\S+$/, 'Please enter a valid email']
    },
    password: {
      type: String,
      required: [true, 'Password is required'],
      minlength: [8, 'Password must be at least 8 characters'],
      select: false
    },
    name: {
      type: String,
      required: [true, 'Name is required'],
      trim: true,
      maxlength: [100, 'Name cannot exceed 100 characters']
    },
    role: {
      type: String,
      enum: ['admin', 'user', 'guest'],
      default: 'user'
    }
  },
  { timestamps: true }
);

// Hash password before saving
UserSchema.pre<IUser>('save', async function (next) {
  if (!this.isModified('password')) return next();
  
  const salt = await bcrypt.genSalt(10);
  this.password = await bcrypt.hash(this.password, salt);
  next();
});

// Method to compare passwords
UserSchema.methods.comparePassword = async function (candidatePassword: string) {
  return await bcrypt.compare(candidatePassword, this.password);
};

// Indexes
UserSchema.index({ email: 1 }, { unique: true });

export default mongoose.model<IUser>('User', UserSchema);
```

#### [36mSequelize Models (PostgreSQL)[0m

```typescript
// user.model.ts
import { Model, DataTypes, Optional } from 'sequelize';
import { sequelize } from '../config/database';

export interface UserAttributes {
  id: number;
  email: string;
  password: string;
  name: string;
  role: 'admin' | 'user' | 'guest';
  createdAt?: Date;
  updatedAt?: Date;
}

interface UserCreationAttributes extends Optional<UserAttributes, 'id' | 'createdAt' | 'updatedAt'> {}

class User extends Model<UserAttributes, UserCreationAttributes> 
  implements UserAttributes {
  public id!: number;
  public email!: string;
  public password!: string;
  public name!: string;
  public role!: 'admin' | 'user' | 'guest';
  public readonly createdAt!: Date;
  public readonly updatedAt!: Date;
}

User.init(
  {
    id: {
      type: DataTypes.INTEGER,
      autoIncrement: true,
      primaryKey: true
    },
    email: {
      type: DataTypes.STRING(255),
      allowNull: false,
      unique: true,
      validate: {
        isEmail: true,
        notEmpty: true
      }
    },
    password: {
      type: DataTypes.STRING(255),
      allowNull: false,
      validate: {
        len: [8, 255]
      }
    },
    name: {
      type: DataTypes.STRING(100),
      allowNull: false,
      validate: {
        notEmpty: true,
        len: [1, 100]
      }
    },
    role: {
      type: DataTypes.ENUM('admin', 'user', 'guest'),
      defaultValue: 'user'
    }
  },
  {
    sequelize,
    modelName: 'User',
    tableName: 'users',
    timestamps: true,
    paranoid: true, // Soft delete
    indexes: [
      {
        unique: true,
        fields: ['email']
      }
    ]
  }
);

export default User;
```

---

## [32m[1m6. TESTING STRATEGY[0m

### 6.1 Testing Pyramid

```
                    ┌─────────────┐
                    │   E2E Tests  │  5-10% of tests
                    │   (Cypress)  │  Test user flows
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ Integration  │  20-30% of tests
                    │   Tests      │  Test API endpoints
                    │   (Jest)     │  Test component interactions
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  Unit Tests  │  60-70% of tests
                    │   (Jest)     │  Test individual functions
                    └─────────────┘
```

### 6.2 Test Examples

#### [36mFrontend Unit Tests (React + Jest)[0m

```typescript
// todo.utils.test.ts
import { formatDate, getTodoStatus } from './todo.utils';

describe('todo.utils', () => {
  describe('formatDate', () => {
    it('should format date correctly', () => {
      const date = new Date('2024-01-15T10:30:00');
      expect(formatDate(date)).toBe('Jan 15, 2024');
    });
    
    it('should handle null date', () => {
      expect(formatDate(null)).toBe('');
    });
  });
  
  describe('getTodoStatus', () => {
    it('should return correct status for completed todo', () => {
      const todo = { id: '1', text: 'Test', completed: true };
      expect(getTodoStatus(todo)).toBe('Completed');
    });
    
    it('should return correct status for active todo', () => {
      const todo = { id: '1', text: 'Test', completed: false };
      expect(getTodoStatus(todo)).toBe('Active');
    });
  });
});
```

```typescript
// TodoItem.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import TodoItem from './TodoItem';

describe('TodoItem', () => {
  const mockTodo = {
    id: '1',
    text: 'Test Todo',
    completed: false
  };
  
  const mockToggle = jest.fn();
  const mockDelete = jest.fn();
  
  it('renders todo item correctly', () => {
    render(
      <TodoItem 
        todo={mockTodo} 
        onToggle={mockToggle} 
        onDelete={mockDelete} 
      />
    );
    
    expect(screen.getByText('Test Todo')).toBeInTheDocument();
    expect(screen.getByRole('checkbox')).not.toBeChecked();
  });
  
  it('calls onToggle when checkbox is clicked', () => {
    render(
      <TodoItem 
        todo={mockTodo} 
        onToggle={mockToggle} 
        onDelete={mockDelete} 
      />
    );
    
    fireEvent.click(screen.getByRole('checkbox'));
    expect(mockToggle).toHaveBeenCalledWith('1');
  });
  
  it('calls onDelete when delete button is clicked', () => {
    render(
      <TodoItem 
        todo={mockTodo} 
        onToggle={mockToggle} 
        onDelete={mockDelete} 
      />
    );
    
    fireEvent.click(screen.getByLabelText('Delete'));
    expect(mockDelete).toHaveBeenCalledWith('1');
  });
});
```

#### [36mBackend Unit Tests (Jest)[0m

```typescript
// todo.service.test.ts
import * as todoService from '../services/todo.service';
import Todo from '../models/todo.model';

// Mock the Todo model
jest.mock('../models/todo.model');

describe('todoService', () => {
  describe('getAllTodos', () => {
    it('should return all todos when no filter is provided', async () => {
      const mockTodos = [
        { id: '1', text: 'Todo 1', completed: false },
        { id: '2', text: 'Todo 2', completed: true }
      ];
      
      (Todo.find as jest.Mock).mockResolvedValue(mockTodos);
      
      const result = await todoService.getAllTodos();
      
      expect(result).toEqual(mockTodos);
      expect(Todo.find).toHaveBeenCalledWith();
    });
    
    it('should filter active todos', async () => {
      const mockTodos = [
        { id: '1', text: 'Todo 1', completed: false }
      ];
      
      const mockQuery = {
        where: jest.fn().mockReturnThis(),
        sort: jest.fn().mockResolvedValue(mockTodos)
      };
      
      (Todo.find as jest.Mock).mockReturnValue(mockQuery);
      
      const result = await todoService.getAllTodos('active');
      
      expect(result).toEqual(mockTodos);
      expect(mockQuery.where).toHaveBeenCalledWith({ completed: false });
    });
  });
  
  describe('createTodo', () => {
    it('should create a new todo', async () => {
      const mockTodo = { id: '1', text: 'New Todo', completed: false };
      const mockSave = jest.fn().mockResolvedValue(mockTodo);
      
      (Todo as jest.Mock).mockImplementation(() => ({
        save: mockSave
      }));
      
      const result = await todoService.createTodo({ text: 'New Todo' });
      
      expect(result).toEqual(mockTodo);
      expect(mockSave).toHaveBeenCalled();
    });
  });
});
```

#### [36mIntegration Tests (Supertest)[0m

```typescript
// todo.routes.test.ts
import request from 'supertest';
import app from '../app';
import Todo from '../models/todo.model';

// Mock the Todo model
jest.mock('../models/todo.model');

describe('Todo Routes', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });
  
  describe('GET /api/todos', () => {
    it('should return all todos', async () => {
      const mockTodos = [
        { id: '1', text: 'Todo 1', completed: false },
        { id: '2', text: 'Todo 2', completed: true }
      ];
      
      (Todo.find as jest.Mock).mockResolvedValue(mockTodos);
      
      const response = await request(app)
        .get('/api/todos')
        .expect(200);
      
      expect(response.body.success).toBe(true);
      expect(response.body.data).toEqual(mockTodos);
    });
    
    it('should filter todos by status', async () => {
      const mockTodos = [
        { id: '1', text: 'Todo 1', completed: false }
      ];
      
      const mockQuery = {
        where: jest.fn().mockReturnThis(),
        sort: jest.fn().mockResolvedValue(mockTodos)
      };
      
      (Todo.find as jest.Mock).mockReturnValue(mockQuery);
      
      const response = await request(app)
        .get('/api/todos?filter=active')
        .expect(200);
      
      expect(response.body.success).toBe(true);
      expect(response.body.data).toEqual(mockTodos);
    });
  });
  
  describe('POST /api/todos', () => {
    it('should create a new todo', async () => {
      const mockTodo = { id: '1', text: 'New Todo', completed: false };
      const mockSave = jest.fn().mockResolvedValue(mockTodo);
      
      (Todo as jest.Mock).mockImplementation(() => ({
        save: mockSave
      }));
      
      const response = await request(app)
        .post('/api/todos')
        .send({ text: 'New Todo' })
        .expect(201);
      
      expect(response.body.success).toBe(true);
      expect(response.body.data).toEqual(mockTodo);
    });
    
    it('should return 400 for invalid input', async () => {
      const response = await request(app)
        .post('/api/todos')
        .send({}) // Empty body
        .expect(400);
      
      expect(response.body.success).toBe(false);
    });
  });
});
```

#### [36mEnd-to-End Tests (Cypress)[0m

```javascript
// cypress/integration/todo.spec.js

describe('Todo Application', () => {
  beforeEach(() => {
    cy.visit('/');
  });
  
  it('should display the todo app title', () => {
    cy.get('h1').should('contain', 'Todo App');
  });
  
  it('should add a new todo', () => {
    const todoText = 'Test Todo';
    
    cy.get('input[type="text"]').type(todoText);
    cy.get('button[type="submit"]').click();
    
    cy.get('.todo-item').should('have.length', 1);
    cy.get('.todo-item').should('contain', todoText);
  });
  
  it('should toggle todo completion', () => {
    // Add a todo first
    cy.get('input[type="text"]').type('Test Todo');
    cy.get('button[type="submit"]').click();
    
    // Toggle the todo
    cy.get('.todo-checkbox').check();
    
    // Verify it's marked as completed
    cy.get('.todo-item').should('have.class', 'completed');
  });
  
  it('should delete a todo', () => {
    // Add a todo first
    cy.get('input[type="text"]').type('Test Todo');
    cy.get('button[type="submit"]').click();
    
    // Delete the todo
    cy.get('.delete-button').click();
    
    // Verify it's removed
    cy.get('.todo-item').should('have.length', 0);
  });
  
  it('should filter todos', () => {
    // Add active and completed todos
    cy.get('input[type="text"]').type('Active Todo');
    cy.get('button[type="submit"]').click();
    
    cy.get('input[type="text"]').type('Completed Todo');
    cy.get('button[type="submit"]').click();
    cy.get('.todo-checkbox').last().check();
    
    // Filter by active
    cy.get('select').select('active');
    cy.get('.todo-item').should('have.length', 1);
    cy.get('.todo-item').should('contain', 'Active Todo');
    
    // Filter by completed
    cy.get('select').select('completed');
    cy.get('.todo-item').should('have.length', 1);
    cy.get('.todo-item').should('contain', 'Completed Todo');
    
    // Show all
    cy.get('select').select('all');
    cy.get('.todo-item').should('have.length', 2);
  });
});
```

---

## [32m[1m7. DEPLOYMENT STRATEGY[0m

### 7.1 Deployment Options

#### [33mFrontend Deployment[0m

| Platform | Free Tier | Features | Best For |
|----------|-----------|----------|----------|
| **Vercel** | ✅ Yes | Auto CI/CD, Preview Deployments | React, Next.js |
| **Netlify** | ✅ Yes | Auto CI/CD, Forms, Functions | All Frontend |
| **GitHub Pages** | ✅ Yes | Simple, GitHub integrated | Static Sites |
| **Firebase Hosting** | ✅ Yes | Fast, CDN, SSL | All Frontend |

**Vercel Deployment Example:**
```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Or with zero-config
vercel --prod
```

**Netlify Deployment Example:**
```bash
# Install Netlify CLI
npm install -g netlify-cli

# Deploy
netlify deploy

# Production deploy
netlify deploy --prod
```

#### [33mBackend Deployment[0m

| Platform | Free Tier | Features | Best For |
|----------|-----------|----------|----------|
| **Render** | ✅ Yes | PostgreSQL, Redis, Easy setup | Node.js, Python |
| **Railway** | ✅ Yes | Multiple databases, Scaling | All Backends |
| **Cyclic** | ✅ Yes | GitHub integration | Node.js |
| **Heroku** | ❌ (Paid) | Mature, Add-ons | All Backends |
| **Fly.io** | ✅ Yes | Docker, Global regions | All Backends |

**Render Deployment Example:**
```yaml
# render.yaml
services:
  - type: web
    name: recruitment-test-backend
    runtime: node
    buildCommand: npm install && npm run build
    startCommand: npm start
    envVars:
      - key: NODE_ENV
        value: production
      - key: DATABASE_URL
        fromService: recruitment-test-db
    autoDeploy: true

  - type: postgres
    name: recruitment-test-db
    plan: free
```

#### [33mFull-Stack Deployment[0m

**Vercel (Frontend) + Render (Backend) Architecture:**
```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   User Browser   │────►│    Vercel        │────►│     Render       │
└─────────────────┘     │   (Frontend)     │     │   (Backend)      │
                        └─────────────────┘     └──────────┬──────┘
                                                             │
                        ┌─────────────────┐     ┌───────────▼──────┐
                        │   PostgreSQL     │◄────│     Render       │
                        │   (Render)       │     │   (Database)     │
                        └─────────────────┘     └─────────────────┘
```

### 7.2 Environment Configuration

**.env.example (Frontend):**
```env
# App
REACT_APP_NAME=Recruitment Test
REACT_APP_VERSION=1.0.0

# API
REACT_APP_API_URL=http://localhost:3001/api

# Analytics (optional)
REACT_APP_GA_TRACKING_ID=
```

**.env.example (Backend):**
```env
# App
NODE_ENV=development
PORT=3001

# Database
DATABASE_URL=mongodb://localhost:27017/recruitment-test

# JWT
JWT_SECRET=your-super-secret-key-here
JWT_EXPIRES_IN=1d
JWT_REFRESH_EXPIRES_IN=7d

# CORS
CORS_ORIGIN=http://localhost:3000

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX=100
```

### 7.3 Docker Configuration (Optional)

**Dockerfile (Frontend):**
```dockerfile
# Build stage
FROM node:18-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Dockerfile (Backend):**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
EXPOSE 3001
CMD ["npm", "start"]
```

**docker-compose.yml (Full-Stack):**
```yaml
version: '3.8'

services:
  frontend:
    build:
      context: ./client
      dockerfile: Dockerfile
    ports:
      - "3000:80"
    environment:
      - REACT_APP_API_URL=http://backend:3001/api
    depends_on:
      - backend

  backend:
    build:
      context: ./server
      dockerfile: Dockerfile
    ports:
      - "3001:3001"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=mongodb://mongo:27017/recruitment-test
      - JWT_SECRET=your-secret-key
    depends_on:
      - mongo

  mongo:
    image: mongo:6
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db
    environment:
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=example

volumes:
  mongo-data:
```

---

## [32m[1m8. EVALUATION RUBRIC[0m

### 8.1 Scoring Breakdown

#### [33mCode Quality (40% - 40 points)[0m

| Criteria | Weight | Excellent (5) | Good (4) | Fair (3) | Poor (2) | Very Poor (1) |
|----------|--------|---------------|----------|---------|---------|---------------|
| **Readability** | 10% | Clean, well-formatted, easy to follow | Mostly clean, minor issues | Some readability issues | Hard to follow | Very difficult to understand |
| **Consistency** | 10% | Consistent style, naming, patterns | Mostly consistent | Some inconsistencies | Many inconsistencies | No consistency |
| **DRY Principle** | 10% | No duplication, well-extracted | Minimal duplication | Some duplication | Significant duplication | Excessive duplication |
| **Error Handling** | 10% | Comprehensive, graceful | Good coverage | Basic handling | Minimal handling | No error handling |

**Code Quality Checklist:**
- [ ] Consistent naming conventions (camelCase, PascalCase, etc.)
- [ ] Proper indentation and formatting
- [ ] Meaningful variable and function names
- [ ] Appropriate use of comments (not too many, not too few)
- [ ] No commented-out code
- [ ] No console.log statements in production code
- [ ] Proper use of TypeScript types (if applicable)
- [ ] No any types (if using TypeScript)
- [ ] Proper error handling at all levels
- [ ] No sensitive information in code

#### [33mFunctionality (30% - 30 points)[0m

| Criteria | Weight | Excellent (5) | Good (4) | Fair (3) | Poor (2) | Very Poor (1) |
|----------|--------|---------------|----------|---------|---------|---------------|
| **Core Features** | 15% | All implemented, working perfectly | All implemented, minor issues | Most implemented | Some implemented | Few implemented |
| **Edge Cases** | 10% | All handled gracefully | Most handled | Some handled | Few handled | None handled |
| **Performance** | 5% | Excellent performance | Good performance | Acceptable | Slow | Very slow |

**Functionality Checklist:**
- [ ] All required features implemented
- [ ] Features work as expected
- [ ] No critical bugs
- [ ] Edge cases handled (empty states, errors, etc.)
- [ ] Loading states implemented
- [ ] Error states handled gracefully
- [ ] Form validation works correctly
- [ ] Data persistence works
- [ ] Responsive design works on all devices
- [ ] Performance meets requirements

#### [33mArchitecture & Design (20% - 20 points)[0m

| Criteria | Weight | Excellent (5) | Good (4) | Fair (3) | Poor (2) | Very Poor (1) |
|----------|--------|---------------|----------|---------|---------|---------------|
| **Structure** | 10% | Logical, well-organized | Mostly logical | Some organization | Poor organization | No organization |
| **Separation of Concerns** | 10% | Excellent separation | Good separation | Some separation | Minimal separation | No separation |

**Architecture Checklist:**
- [ ] Logical project structure
- [ ] Proper separation of concerns
- [ ] Modular code
- [ ] Reusable components/functions
- [ ] Appropriate use of design patterns
- [ ] Scalable architecture
- [ ] Proper use of frameworks/libraries
- [ ] Clean component hierarchy
- [ ] Proper state management
- [ ] Good API design (if applicable)

#### [33mDocumentation (10% - 10 points)[0m

| Criteria | Weight | Excellent (5) | Good (4) | Fair (3) | Poor (2) | Very Poor (1) |
|----------|--------|---------------|----------|---------|---------|---------------|
| **README** | 5% | Comprehensive, clear, helpful | Good coverage | Basic coverage | Minimal coverage | No README |
| **Code Comments** | 5% | Helpful, not excessive | Appropriate | Some comments | Few comments | No comments |

**Documentation Checklist:**
- [ ] README.md with project description
- [ ] Features implemented listed
- [ ] Technology stack documented
- [ ] Setup instructions clear and accurate
- [ ] Running instructions provided
- [ ] Testing instructions included
- [ ] Deployment notes (if applicable)
- [ ] Screenshots included
- [ ] Code comments where necessary
- [ ] API documentation (if applicable)
- [ ] Design decisions explained

### 8.2 Scoring Tiers

| Total Score | Tier | Description |
|-------------|------|-------------|
| 90-100 | **Exceptional** | Exceeds all expectations, production-ready |
| 80-89 | **Excellent** | Very high quality, minor improvements needed |
| 70-79 | **Good** | Solid implementation, some improvements needed |
| 60-69 | **Fair** | Meets basic requirements, significant improvements needed |
| 50-59 | **Poor** | Below expectations, major improvements needed |
| <50 | **Rejected** | Does not meet minimum requirements |

### 8.3 Bonus Points (Up to 10 points)

| Bonus Feature | Points | Description |
|---------------|--------|-------------|
| **User Authentication** | +2 | Full auth system with JWT |
| **Real-time Updates** | +2 | WebSocket or polling implementation |
| **Advanced Search** | +1 | Full-text search, filters |
| **Pagination** | +1 | Proper pagination implementation |
| **Testing >90%** | +2 | Exceptional test coverage |
| **Docker Setup** | +1 | Docker configuration included |
| **CI/CD Pipeline** | +1 | GitHub Actions or similar |

---

## [32m[1m9. PROJECT TEMPLATES[0m

### 9.1 Quick Start Templates

#### [36mReact + TypeScript + Vite (Recommended)[0m

```bash
# Create project
npm create vite@latest my-recruitment-test -- --template react-ts
cd my-recruitment-test

# Install additional dependencies
npm install @tanstack/react-query axios react-router-dom zustand
npm install -D @testing-library/react @testing-library/jest-dom @types/jest

# Initialize Git
git init
git add .
git commit -m "Initial project setup"

# Create folder structure
mkdir -p src/{components/{common,layout,features},pages,hooks,services,utils,styles}
```

**package.json scripts:**
```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test": "vitest",
    "test:coverage": "vitest run --coverage",
    "lint": "eslint src --ext ts,tsx",
    "lint:fix": "eslint src --ext ts,tsx --fix",
    "format": "prettier --write \"src/**/*.{ts,tsx,css,json}\""
  }
}
```

#### [36mExpress + TypeScript (Backend)[0m

```bash
# Create project
mkdir server
cd server
npm init -y

# Install dependencies
npm install express mongoose cors dotenv helmet morgan bcryptjs jsonwebtoken
npm install -D typescript @types/express @types/mongoose @types/cors ts-node nodemon

# Initialize TypeScript
npx tsc --init

# Create folder structure
mkdir -p src/{config,controllers,middlewares,models,routes,services,utils,types}
mkdir -p tests/{unit,integration}
```

**tsconfig.json:**
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "tests"]
}
```

**package.json scripts:**
```json
{
  "scripts": {
    "dev": "nodemon src/server.ts",
    "build": "tsc",
    "start": "node dist/server.js",
    "test": "jest",
    "test:coverage": "jest --coverage",
    "lint": "eslint src --ext ts",
    "lint:fix": "eslint src --ext ts --fix"
  }
}
```

---

## [32m[1m10. CHECKLISTS[0m

### 10.1 Pre-Submission Checklist

**Code Quality:**
- [ ] All code is properly formatted
- [ ] No console.log statements in production code
- [ ] No commented-out code
- [ ] No sensitive information (API keys, passwords)
- [ ] Consistent naming conventions
- [ ] Proper TypeScript types (if applicable)
- [ ] No any types (if using TypeScript)
- [ ] Proper error handling
- [ ] Code follows DRY principle

**Functionality:**
- [ ] All required features implemented
- [ ] All features tested manually
- [ ] Edge cases handled
- [ ] Loading states implemented
- [ ] Error states handled
- [ ] Form validation works
- [ ] Data persistence works
- [ ] Responsive design works

**Testing:**
- [ ] Unit tests written for critical functions
- [ ] Integration tests written for API endpoints
- [ ] E2E tests written for user flows (optional)
- [ ] Test coverage >= 70%
- [ ] All tests passing

**Documentation:**
- [ ] README.md completed
- [ ] Project description included
- [ ] Features implemented listed
- [ ] Technology stack documented
- [ ] Setup instructions clear
- [ ] Running instructions provided
- [ ] Testing instructions included
- [ ] Screenshots added
- [ ] Code comments where necessary

**Git:**
- [ ] Regular, meaningful commits
- [ ] Proper branch naming
- [ ] .gitignore file present
- [ ] No sensitive data in repository
- [ ] No node_modules in repository
- [ ] No build artifacts in repository

### 10.2 Final Review Checklist

**Before Submission:**
- [ ] Run linter and fix all issues
- [ ] Run formatter on all files
- [ ] Run all tests and verify passing
- [ ] Test on different browsers
- [ ] Test on different screen sizes
- [ ] Verify build process works
- [ ] Verify deployment works (if applicable)
- [ ] Check for typos in documentation
- [ ] Verify all links in README work
- [ ] Remove any hardcoded sensitive data

---

## [32m[1m11. RESOURCES & REFERENCES[0m

### 11.1 Learning Resources

**Frontend:**
- [React Documentation](https://react.dev/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/)
- [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [Zustand Documentation](https://docs.pmnd.rs/zustand/getting-started/introduction)
- [Redux Toolkit](https://redux-toolkit.js.org/)

**Backend:**
- [Express.js Documentation](https://expressjs.com/)
- [Mongoose Documentation](https://mongoosejs.com/)
- [Sequelize Documentation](https://sequelize.org/)
- [JWT Handbook](https://jwt.io/introduction)
- [bcrypt Documentation](https://github.com/kelektiv/node.bcrypt.js)

**Testing:**
- [Jest Documentation](https://jestjs.io/)
- [Cypress Documentation](https://docs.cypress.io/)
- [Supertest Documentation](https://github.com/visionmedia/supertest)

**Deployment:**
- [Vercel Documentation](https://vercel.com/docs)
- [Netlify Documentation](https://docs.netlify.com/)
- [Render Documentation](https://render.com/docs)
- [Docker Documentation](https://docs.docker.com/)

### 11.2 Tools & Extensions

**VS Code Extensions:**
- ESLint
- Prettier
- TypeScript Toolbox
- GitLens
- Jest
- Thunder Client (API testing)
- Docker

**Online Tools:**
- [JSON Formatter](https://jsonformatter.curiousconcept.com/)
- [Regex Tester](https://regex101.com/)
- [Color Picker](https://colorpicker.me/)
- [API Mocking](https://mockapi.io/)

---

## [32m[1m12. FAQ & TROUBLESHOOTING[0m

### 12.1 Common Issues

**Q: I'm getting CORS errors when calling my API.**
A: Make sure your backend has CORS enabled:
```typescript
// Express.js
import cors from 'cors';
app.use(cors({
  origin: 'http://localhost:3000',
  credentials: true
}));
```

**Q: My TypeScript types are not working.**
A: Check your tsconfig.json and ensure you have proper type definitions installed. For third-party libraries, install their types:
```bash
npm install -D @types/library-name
```

**Q: My tests are not running.**
A: Make sure you have the correct test dependencies installed and your test scripts are configured properly. For Jest:
```bash
npm install -D jest @types/jest ts-jest
```

**Q: My application is slow.**
A: Check for:
- Unnecessary re-renders in React (use React.memo, useCallback)
- Large bundle size (use code splitting, lazy loading)
- Inefficient database queries (add indexes, optimize queries)
- Missing loading states

**Q: I'm getting authentication errors.**
A: Common issues:
- JWT secret mismatch between frontend and backend
- Token not being sent with requests
- Token expired
- CORS blocking credentials

### 12.2 Getting Help

If you're stuck:
1. Check the official documentation for the technology you're using
2. Search Stack Overflow
3. Review the requirements and this design plan
4. Start with a simpler approach and build up
5. Focus on getting core features working first

---

## [32m[1m13. APPENDIX[0m

### 13.1 Sample Project: Todo App Implementation Guide

**Step 1: Setup**
```bash
npm create vite@latest todo-app -- --template react-ts
cd todo-app
npm install zustand uuid
npm install -D @testing-library/react @testing-library/jest-dom
```

**Step 2: Create Todo Type**
```typescript
// src/types/todo.ts
export interface Todo {
  id: string;
  text: string;
  completed: boolean;
  createdAt: Date;
}

export type TodoFilter = 'all' | 'active' | 'completed';
```

**Step 3: Create Todo Store**
```typescript
// src/stores/todoStore.ts
import { create } from 'zustand';
import { persist } from 'zustand/middleware';
import { Todo, TodoFilter } from '../types/todo';
import { v4 as uuidv4 } from 'uuid';

interface TodoState {
  todos: Todo[];
  filter: TodoFilter;
  addTodo: (text: string) => void;
  toggleTodo: (id: string) => void;
  deleteTodo: (id: string) => void;
  setFilter: (filter: TodoFilter) => void;
}

export const useTodoStore = create<TodoState>()(
  persist(
    (set) => ({
      todos: [],
      filter: 'all',
      addTodo: (text) => set((state) => ({
        todos: [...state.todos, {
          id: uuidv4(),
          text,
          completed: false,
          createdAt: new Date()
        }]
      })),
      toggleTodo: (id) => set((state) => ({
        todos: state.todos.map((todo) =>
          todo.id === id ? { ...todo, completed: !todo.completed } : todo
        )
      })),
      deleteTodo: (id) => set((state) => ({
        todos: state.todos.filter((todo) => todo.id !== id)
      })),
      setFilter: (filter) => set({ filter })
    }),
    {
      name: 'todo-storage'
    }
  )
);
```

**Step 4: Create Components**
```typescript
// src/components/TodoForm.tsx
import { useState } from 'react';
import { useTodoStore } from '../stores/todoStore';

export const TodoForm = () => {
  const [text, setText] = useState('');
  const addTodo = useTodoStore((state) => state.addTodo);
  
  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    if (text.trim()) {
      addTodo(text.trim());
      setText('');
    }
  };
  
  return (
    <form onSubmit={handleSubmit} className="todo-form">
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
        placeholder="Add a new todo..."
      />
      <button type="submit">Add</button>
    </form>
  );
};
```

### 13.2 Sample Project: Blog Platform API Guide

**Step 1: Setup Express Server**
```typescript
// src/server.ts
import express from 'express';
import cors from 'cors';
import mongoose from 'mongoose';
import dotenv from 'dotenv';
import postRoutes from './routes/post.routes';
import userRoutes from './routes/user.routes';
import authRoutes from './routes/auth.routes';
import { errorHandler } from './middlewares/error.middleware';

dotenv.config();

const app = express();

// Middleware
app.use(cors());
app.use(express.json());

// Routes
app.use('/api/posts', postRoutes);
app.use('/api/users', userRoutes);
app.use('/api/auth', authRoutes);

// Error handling
app.use(errorHandler);

// Database connection
mongoose.connect(process.env.DATABASE_URL!)
  .then(() => console.log('Connected to database'))
  .catch((err) => console.error('Database connection error:', err));

const PORT = process.env.PORT || 3001;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**Step 2: Create Post Model**
```typescript
// src/models/post.model.ts
import mongoose, { Document, Schema } from 'mongoose';

export interface IPost extends Document {
  title: string;
  content: string;
  slug: string;
  status: 'draft' | 'published' | 'archived';
  user: mongoose.Types.ObjectId;
  tags: string[];
  createdAt: Date;
  updatedAt: Date;
}

const PostSchema = new Schema<IPost>(
  {
    title: { type: String, required: true, trim: true },
    content: { type: String, required: true },
    slug: { type: String, required: true, unique: true, trim: true },
    status: {
      type: String,
      enum: ['draft', 'published', 'archived'],
      default: 'draft'
    },
    user: { type: Schema.Types.ObjectId, ref: 'User', required: true },
    tags: { type: [String], default: [] }
  },
  { timestamps: true }
);

// Generate slug before saving
PostSchema.pre<IPost>('save', function (next) {
  if (this.isModified('title')) {
    this.slug = this.title.toLowerCase().replace(/\s+/g, '-');
  }
  next();
});

// Indexes
PostSchema.index({ title: 'text', content: 'text' });
PostSchema.index({ user: 1 });
PostSchema.index({ status: 1 });

export default mongoose.model<IPost>('Post', PostSchema);
```

---

## [32m[1m14. CONCLUSION[0m

This design plan provides a comprehensive framework for the Mistral AI Web Application Recruitment Test. It outlines the technical requirements, architecture patterns, implementation strategies, and evaluation criteria to ensure a fair and consistent assessment process.

**Key Takeaways:**
1. **Choose the right project level** based on your experience and available time
2. **Focus on quality over quantity** - better to have fewer features done well
3. **Follow best practices** in code organization, testing, and documentation
4. **Test thoroughly** - both manually and with automated tests
5. **Document everything** - make it easy for evaluators to understand your work

**Success Criteria:**
- Clean, maintainable code
- Working features that meet requirements
- Good architecture and design decisions
- Comprehensive documentation
- Thorough testing

By following this design plan, candidates can create a high-quality submission that effectively demonstrates their web development skills.

---

*Design Plan Version: 1.0*
*Last Updated: 2024*
*Author: Vibe Code (Mistral AI)*
*Inspired by: Test Gorillas, HackerRank, and industry best practices*

---

## [34m[1mQuick Navigation[0m

- [Executive Summary](#1-executive-summary)
- [Architecture Overview](#2-architecture-overview)
- [Technical Specifications](#3-technical-specifications)
- [Implementation Roadmap](#4-implementation-roadmap)
- [Detailed Technical Guidelines](#5-detailed-technical-guidelines)
- [Testing Strategy](#6-testing-strategy)
- [Deployment Strategy](#7-deployment-strategy)
- [Evaluation Rubric](#8-evaluation-rubric)
- [Project Templates](#9-project-templates)
- [Checklists](#10-checklists)
- [Resources & References](#11-resources--references)
- [FAQ & Troubleshooting](#12-faq--troubleshooting)
- [Appendix](#13-appendix)

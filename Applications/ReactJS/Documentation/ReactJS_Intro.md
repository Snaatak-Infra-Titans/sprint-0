# React — Introduction

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is React?](#2-what-is-react)
3. [Why React?](#3-why-react)
4. [Key Features](#4-key-features)
5. [React in OT-Microservices](#5-react-in-ot-microservices)
6. [Conclusion](#6-conclusion)
7. [Contact Information](#7-contact-information)
8. [References](#8-references)

---

## 1. Introduction

Modern web applications are expected to be fast, dynamic, and responsive — updating content in real time without full page reloads, handling complex user interactions, and working consistently across browsers and devices. Building this kind of experience with raw HTML, CSS, and JavaScript quickly becomes unmanageable as the application grows.

**React** was created to solve exactly this problem — providing a structured, component-based way to build interactive user interfaces that scale cleanly from a simple widget to a full enterprise dashboard.

> **In the context of OT-Microservices:** React powers the **Frontend** — the browser-based dashboard that visualizes employee data, attendance records, and salary information by consuming the Go, Python, and Java backend APIs.

---

## 2. What is React?

**React** (also called **React.js**) is an open-source **JavaScript library** for building user interfaces. It was created by **Jordan Walke** at Facebook and first deployed on Facebook's News Feed in 2011. It was open-sourced in 2013 and has since become the most widely used frontend library in the world.

| Attribute | Detail |
|-----------|--------|
| **Full Name** | React / React.js |
| **Developed By** | Meta (Facebook) — now open-source |
| **First Released** | 2013 |
| **Language** | JavaScript (with optional TypeScript support) |
| **License** | MIT |
| **Type** | UI Library (not a full framework) |
| **Package** | `npm install react react-dom` |
| **Version Check** | Listed in `package.json` under `dependencies` |
| **Official Site** | https://react.dev |

### 2.1 Library vs Framework

React is intentionally described as a **library**, not a framework. This distinction matters:

| | Library (React) | Framework (Angular, Vue) |
|-|-----------------|--------------------------|
| **Scope** | Handles UI rendering only | Handles routing, state, HTTP, forms — everything |
| **Flexibility** | You choose every other tool | The framework decides the tools |
| **Learning curve** | Smaller core to learn | More to learn upfront, but more built-in |
| **Control** | You are in charge of the architecture | Framework enforces structure |

React focuses exclusively on the **View** layer — rendering UI from data. Everything else (routing, API calls, state management) is handled by the developer's choice of companion libraries like React Router, Axios, or Redux.

### 2.2 What Does React Actually Produce?

React applications compile down to standard HTML, CSS, and JavaScript files. The output of `npm run build` is a `build/` folder containing:

```
build/
├── index.html              ← The single HTML page
├── static/
│   ├── js/main.[hash].js   ← All React components bundled into one JS file
│   └── css/main.[hash].css ← All styles bundled
└── asset-manifest.json
```

This output is served by Nginx as static files. The browser downloads the JavaScript bundle, React initializes in the browser, and from that point forward the application updates the page dynamically without full reloads.

---

## 3. Why React?

### 3.1 The Problem with Traditional Web Development

In traditional web development, every user interaction that needed to update the page required one of:

- A full page reload (slow, loses scroll position and form state)
- Direct DOM manipulation with JavaScript (`document.getElementById`, `innerHTML`) — complex, error-prone, and hard to maintain at scale

As applications grew larger, directly manipulating the DOM became the primary source of bugs. Keeping the UI in sync with the underlying data was entirely the developer's responsibility — with no systematic approach.

### 3.2 How React Solves This

React introduces two fundamental ideas that change how UIs are built:

**1. Declarative UI**
Instead of writing instructions for *how* to update the DOM, you describe *what* the UI should look like for a given state. React figures out what changed and updates only what is necessary.

```jsx
// Imperative (traditional JavaScript) — you manage every DOM change
if (isLoggedIn) {
    document.getElementById('greeting').innerText = 'Welcome back!';
    document.getElementById('login-btn').style.display = 'none';
} else {
    document.getElementById('greeting').innerText = 'Please log in';
    document.getElementById('login-btn').style.display = 'block';
}

// Declarative (React) — describe what to render, React handles the DOM
function Header({ isLoggedIn }) {
    return (
        <div>
            <p>{isLoggedIn ? 'Welcome back!' : 'Please log in'}</p>
            {!isLoggedIn && <button>Login</button>}
        </div>
    );
}
```

**2. Component-Based Architecture**
The UI is broken into small, reusable, self-contained **components**. Each component manages its own logic and rendering. Complex UIs are built by composing simple components together — exactly like building with blocks.

### 3.3 Why React Over Alternatives?

| Framework / Library | Strengths | Consideration |
|---------------------|-----------|---------------|
| **React** | Largest ecosystem, most jobs, flexible, backed by Meta | Library only — need to choose routing/state tools separately |
| **Angular** | Full framework, strong TypeScript support, opinionated structure | Steeper learning curve, more verbose |
| **Vue.js** | Gentle learning curve, good documentation, balanced approach | Smaller ecosystem than React |
| **Svelte** | Compiles to vanilla JS, no virtual DOM overhead, very fast | Smaller community, fewer enterprise adoptions |
| **Next.js** | Server-side rendering, built on React | Adds complexity for simple SPAs |

React's combination of the largest community, the richest ecosystem of third-party libraries, and the backing of Meta makes it the dominant choice for new projects — particularly in organizations that need a large talent pool.

---

## 4. Key Features

### 4.1 Component-Based Architecture

Everything in React is a **component** — a self-contained piece of UI with its own logic, state, and rendering. Components can be as small as a button or as large as an entire page.

```jsx
// A simple functional component
function EmployeeCard({ name, designation, location }) {
    return (
        <div className="card">
            <h3>{name}</h3>
            <p>{designation}</p>
            <p>{location}</p>
        </div>
    );
}

// Composed into a list component
function EmployeeList({ employees }) {
    return (
        <div>
            {employees.map(emp => (
                <EmployeeCard
                    key={emp.id}
                    name={emp.name}
                    designation={emp.designation}
                    location={emp.office_location}
                />
            ))}
        </div>
    );
}
```

**Benefits of components:**

| Benefit | Explanation |
|---------|-------------|
| **Reusability** | Write once, use the same component in multiple places |
| **Isolation** | A bug in one component does not crash others |
| **Testability** | Each component can be tested independently |
| **Maintainability** | Large applications are easier to reason about when split into focused components |

### 4.2 JSX — JavaScript + HTML Syntax

React uses **JSX** (JavaScript XML) — a syntax extension that lets you write HTML-like markup directly inside JavaScript. JSX is not valid JavaScript on its own; it is transpiled to regular JavaScript by tools like Babel during the build process.

```jsx
// JSX (what developers write)
const element = (
    <div className="container">
        <h1>Hello, {username}!</h1>
        <p>You have {messages.length} new messages.</p>
    </div>
);

// What Babel compiles it to (what the browser actually runs)
const element = React.createElement('div', { className: 'container' },
    React.createElement('h1', null, 'Hello, ', username, '!'),
    React.createElement('p', null, 'You have ', messages.length, ' new messages.')
);
```

JSX makes component code readable and intuitive — the structure of the JSX mirrors the structure of the rendered HTML.

### 4.3 Virtual DOM

The **Virtual DOM** is one of React's most important performance innovations. Instead of updating the real browser DOM directly (which is slow), React:

1. Maintains a lightweight in-memory copy of the DOM — the **Virtual DOM**
2. When state changes, React creates a new Virtual DOM tree
3. React **diffs** the old and new Virtual DOM trees to find what changed (this is called **reconciliation**)
4. Only the changed parts are updated in the real DOM — not the whole page

```
State Changes
      │
      ▼
React re-renders component → New Virtual DOM
      │
      ▼
Diff: New Virtual DOM vs Previous Virtual DOM
      │
      ▼
Minimal set of real DOM updates applied
      │
      ▼
Browser repaints only what changed ✅
```

This makes React applications feel fast even when managing large amounts of dynamic data — like a table of hundreds of employees updating in real time.

### 4.4 State and Props

React components communicate and manage data through two mechanisms:

**Props (Properties)** — data passed *into* a component from its parent. Props are read-only — a component cannot modify its own props.

```jsx
// Parent passes data down via props
<EmployeeCard name="John Smith" designation="Developer" />

// Child receives and uses props
function EmployeeCard({ name, designation }) {
    return <div>{name} — {designation}</div>;
}
```

**State** — data that lives *inside* a component and can change over time. When state changes, React re-renders the component automatically.

```jsx
import { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);  // initial state = 0

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
    );
}
```

| | Props | State |
|-|-------|-------|
| **Owned by** | Parent component | The component itself |
| **Mutable?** | No — read only | Yes — via setter function |
| **Purpose** | Pass data down the tree | Track internal, changing data |
| **Triggers re-render?** | Yes, when parent re-renders | Yes, when state is updated |

### 4.5 Hooks

**Hooks** were introduced in React 16.8 and transformed how React components are written. Hooks are functions that let functional components use React features that previously required class components.

The most important built-in hooks:

| Hook | Purpose | Example Use |
|------|---------|-------------|
| `useState` | Add local state to a functional component | Track form input values, toggle visibility |
| `useEffect` | Run side effects after render | Fetch API data on component mount |
| `useContext` | Access shared global state | User authentication, theme settings |
| `useRef` | Reference a DOM element directly | Focus an input, store a timer ID |
| `useMemo` | Cache expensive calculations | Avoid re-computing derived data |
| `useCallback` | Cache a function reference | Prevent unnecessary child re-renders |

**Example — fetching employee data with hooks (pattern used in OT-Microservices):**

```jsx
import { useState, useEffect } from 'react';

function EmployeeList() {
    const [employees, setEmployees] = useState([]);   // state: list of employees
    const [loading, setLoading]     = useState(true); // state: loading flag

    useEffect(() => {
        // Runs once after the component mounts
        fetch('/employee/search/all')
            .then(res => res.json())
            .then(data => {
                setEmployees(Array.isArray(data) ? data : []);
                setLoading(false);
            })
            .catch(() => setLoading(false));
    }, []); // empty array = run once on mount only

    if (loading) return <p>Loading...</p>;

    return (
        <ul>
            {employees.map(emp => (
                <li key={emp.id}>{emp.name} — {emp.designation}</li>
            ))}
        </ul>
    );
}
```

### 4.6 Unidirectional Data Flow

React enforces a **one-way data flow** — data always flows from parent to child via props, never the other way. This makes the data flow in an application predictable and easy to debug.

```
App (top-level state)
  │
  │  props
  ▼
EmployeeList
  │
  │  props
  ▼
EmployeeCard
```

If a child needs to communicate back to its parent (e.g., a form submission), the parent passes a **callback function** down as a prop, which the child calls when needed.

### 4.7 React Router

React is a single-page application (SPA) library — by default, there is only one HTML page. **React Router** is the standard companion library that adds client-side routing, making different URLs render different components without a page reload.

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
    return (
        <BrowserRouter>
            <Routes>
                <Route path="/"               element={<HomePage />} />
                <Route path="/employee-list"  element={<EmployeeList />} />
                <Route path="/attendance"     element={<AttendanceList />} />
                <Route path="/salary"         element={<ListSalary />} />
            </Routes>
        </BrowserRouter>
    );
}
```

### 4.8 Rich Ecosystem

React's library ecosystem covers virtually every UI need:

| Category | Popular Libraries |
|----------|------------------|
| Routing | React Router, TanStack Router |
| State Management | Redux, Zustand, Recoil, Context API |
| UI Component Libraries | Material UI, Ant Design, Tabler (used in OT-Microservices), Chakra UI |
| Form Management | Formik (used in OT-Microservices), React Hook Form |
| Data Fetching | Axios, TanStack Query, SWR |
| Testing | React Testing Library, Jest |
| Charts & Visualization | Recharts, Chart.js, Victory |

### 4.9 Single Page Application (SPA)

React applications are **Single Page Applications**. The browser loads one HTML file once, and all subsequent navigation is handled by JavaScript — no full page reloads.

| Traditional Multi-Page App | React SPA |
|---------------------------|-----------|
| Each navigation = full page reload | Navigation updates only what changed |
| Server renders each page | Browser renders everything |
| Slower perceived navigation | Instant navigation after initial load |
| Simpler SEO (server sends full HTML) | SEO needs extra configuration (SSR/SSG) |

For internal tools like the OT-Microservices dashboard — where SEO is not a concern — the SPA model is ideal.

---

## 5. React in OT-Microservices

In the OT-Microservices project, React is used for the **Frontend** — the browser dashboard that consumes the three backend APIs.

### 5.1 Key Details

| Attribute | Detail |
|-----------|--------|
| **React Version** | 16.x (uses class components alongside functional components) |
| **Port (Dev)** | 3000 (`npm start`) |
| **Port (Prod)** | 80 (served by Nginx from the `build/` folder) |
| **UI Library** | Tabler React (dashboard components) |
| **Form Library** | Formik (form state management) |
| **Node.js Version** | 18.x (required) |
| **Build Tool** | Webpack 4 (via `react-scripts` 2.0.3) |
| **Build Command** | `npm run build` |

### 5.2 Component Map

| Component File | What It Renders |
|----------------|----------------|
| `App.react.js` | Top-level router — maps URLs to pages |
| `HomePage.react.js` | Main dashboard with stat cards |
| `EmployeeData.js` | Total / Active / Ex-Employee stat cards |
| `EmployeeList.js` | Table of all employees |
| `EmployeeForm.js` | Add new employee form (Formik) |
| `AttendanceList.js` | Table of all attendance records |
| `AttendanceForm.js` | Add attendance record form |
| `ListSalary.js` | Table of all salary records |
| `SiteWrapper.react.js` | Navigation sidebar and page layout |

### 5.3 How the Frontend Talks to the Backends

React components call the backend APIs using the browser's `fetch` API. Nginx acts as a reverse proxy, routing requests to the correct backend service based on the URL prefix:

```
React component calls:     Nginx routes to:
/employee/search/all   →   Go API     (port 8080)
/attendance/search/all →   Python API (port 8081)
/salary/search/all     →   Java API   (port 8082)
```

### 5.4 Build and Deploy Flow

```
1. Developer edits files in ~/frontend/src/
         │
         ▼
2. npm run build
   (Webpack bundles all JS/CSS into ~/frontend/build/)
         │
         ▼
3. Nginx serves ~/frontend/build/index.html at port 80
         │
         ▼
4. Browser loads index.html → downloads JS bundle
         │
         ▼
5. React initializes in the browser
         │
         ▼
6. Components fetch data from backend APIs via Nginx
```

> **Important:** Every change to source files in `src/` requires a fresh `npm run build` before it is visible through Nginx. The development server (`npm start`) is not used in production.

---

## 6. Conclusion

React's component model, Virtual DOM, declarative rendering, and rich ecosystem make it the leading choice for building modern web UIs. Its focus on the View layer gives developers the flexibility to build everything from a simple widget to a complex multi-page dashboard.

Key takeaways:

- React is a **UI library**, not a framework — it handles rendering, you choose everything else
- **Components** are the building blocks — self-contained, reusable, and composable
- The **Virtual DOM** ensures only the minimal set of real DOM changes are made, keeping the UI fast
- **Props** pass data down; **State** tracks changing data inside a component
- **Hooks** (`useState`, `useEffect`) are the modern way to manage state and side effects in functional components
- **Unidirectional data flow** makes applications predictable and easier to debug
- In OT-Microservices, React renders the **Frontend dashboard** — served by Nginx from the compiled `build/` folder — and consumes all three backend APIs

---

## 7. Contact Information

| Name | Role | Email |
|------|------|-------|
| Deepak | Author | deepak.nagar.snaatak@mygurukulam.co |

---

## 8. References

| Resource | Link |
|----------|------|
| React Official Documentation | https://react.dev |
| React Legacy Docs (v16/17) | https://legacy.reactjs.org |
| React Router Documentation | https://reactrouter.com |
| Formik Documentation | https://formik.org |
| Tabler React UI Library | https://tabler.io/docs |
| Create React App | https://create-react-app.dev |
| OT-Microservices Frontend | https://github.com/OT-MICROSERVICES/frontend |

---

*Author: Deepak | Sprint 0 | Infra-Titans | April 2026*

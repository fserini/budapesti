# Frontend Documentation

## 1. Introduction

The Budapesti frontend is a **mobile-first web application** built with **React**, **TypeScript**, and **Vite**. It provides the user interface for tourists to explore Budapest — including an interactive map, points of interest, and a personal checklist. The frontend communicates with the backend API to fetch and display data.

---

## 2. Objective

The goal of the frontend is to:

- Provide a responsive, mobile-friendly UI for tourists
- Display an interactive map with Points of Interest
- Allow users to manage a personal visit checklist
- Communicate with the backend REST API

---

## 3. Technologies Used

| Technology   | Purpose                                                 |
|--------------|---------------------------------------------------------|
| React 18     | Component-based UI library                             |
| TypeScript   | Typed superset of JavaScript — catches errors early     |
| Vite         | Fast development server and build tool                 |
| React DOM    | Renders React components into the browser DOM          |

---

## 4. Project Structure Explanation

```
frontend/
├── index.html              # HTML entry point — Vite injects the JS bundle here
├── package.json            # Node.js dependencies and scripts
├── tsconfig.json           # TypeScript compiler configuration
├── vite.config.ts          # Vite configuration (dev server, proxy, plugins)
└── src/
    ├── main.tsx            # Application bootstrap — mounts React into #root
    ├── App.tsx             # Root component — top-level routing and layout
    ├── components/         # Reusable UI building blocks (buttons, cards, etc.)
    ├── pages/              # Full-page components, one per route (e.g. MapPage)
    │   └── MapPage.tsx     # Placeholder for the interactive map view
    ├── services/           # API call functions (fetch/axios wrappers)
    ├── hooks/              # Custom React hooks (reusable stateful logic)
    └── types/              # TypeScript type definitions and interfaces
```

**Why this structure?**  
This is a commonly used structure in React projects. It separates concerns clearly:
- **pages/** contain screen-level components that correspond to app routes.
- **components/** hold smaller, reusable elements shared across pages.
- **services/** centralise all API calls so they are easy to maintain and mock in tests.
- **hooks/** extract complex stateful logic from components, keeping them clean.
- **types/** define shared TypeScript interfaces, making the codebase type-safe.

---

## 5. How It Works (High-Level)

1. When a user opens the app, the browser loads `index.html`.
2. Vite serves the JS bundle, which executes `main.tsx`.
3. `main.tsx` renders the `<App />` component inside the `#root` DOM element.
4. `App.tsx` acts as the shell — it defines the layout and renders `<MapPage />`.
5. In development, Vite proxies all `/api/*` requests to `http://localhost:8080` (the backend), so the frontend and backend can run independently without CORS issues.

---

## 6. Design Decisions

- **React** is the most widely adopted UI library — a great choice for learning modern frontend development.
- **TypeScript** is strongly recommended over plain JavaScript for any non-trivial project. It provides autocomplete, catches type errors at compile time, and makes the codebase more maintainable.
- **Vite** was chosen over Create React App because it is significantly faster for both startup and hot-module replacement.
- **Mobile-first design** means styles are written for small screens first, then scaled up with media queries — ensuring a good experience for tourists using their phones.
- **Proxy configuration in vite.config.ts** removes the need to configure CORS during development.

---

## 7. Best Practices

- **Use TypeScript types/interfaces** to define the shape of all API responses in `types/`.
- **Keep components small and focused** — a component should do one thing.
- **Extract repeated logic** into custom hooks in `hooks/`.
- **Never call the API directly from a component** — use a `services/` function instead.
- **Use React.FC with explicit props types** to improve readability and type safety.
- **Avoid prop drilling** — for shared state, consider React Context or a state management library.
- **Test components** using React Testing Library to simulate user interactions.

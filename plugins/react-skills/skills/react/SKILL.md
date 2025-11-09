---
name: react
description: React development best practices and patterns, including modern data fetching with React 19.
---

# React Development

Modern React development patterns and best practices.

## Data Fetching

Use React 19's `use` hook with `Suspense` for data fetching. Don't use `useEffect` for fetching data.

### Basic Data Fetching

```tsx
import { use } from "react";

const fetchUsers = fetch('/api/users').then(res => {
  if (!res.ok) {
    throw new Error(`HTTP error! status: ${res.status}`);
  }
  return res.json();
});

export function Users() {
  const users = use(fetchUsers);
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

### Loading States with Suspense

Wrap components with `Suspense` for loading states:

```tsx
import { Suspense } from "react";
import { Users } from "./pages/Users";

export function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Users />
    </Suspense>
  );
}
```

## Guidelines

- Use the `use` hook for data fetching instead of `useEffect`
- Always wrap data-fetching components with `Suspense` boundaries
- Handle errors properly in your fetch promises
- Prefer declarative data fetching patterns over imperative ones

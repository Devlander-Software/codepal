

# **Component Folder Structure Documentation**

This document serves as a detailed guide for organizing and developing UI components, state management, queries, and mutations in a project using the **Atomic Design methodology**. It includes best practices for ensuring **separation of concerns**, scalability, and maintainability, tailored for a **Next.js project** with React Query and modern design-system principles.

---

## **Philosophy Behind the Structure**

The **Atomic Design methodology** and **separation of concerns** ensure the project is:
1. **Modular**: Components and logic are decoupled and reusable.
2. **Scalable**: Adding new features or pages doesn't compromise existing code.
3. **Maintainable**: Each layer of the application is clearly defined, with no overlap of responsibilities.

This structure prioritizes **presentational purity** for UI components and isolates application logic (e.g., state management, data fetching) into containers, hooks, or context.

---

## **Folder Structure**

### Root Structure
```
src/
├── app/                     # Next.js App Router files
├── components/              # Atomic design components
│   ├── atoms/
│   ├── molecules/
│   ├── organisms/
│   ├── templates/
├── containers/              # Stateful components (connect logic to UI)
├── state/                   # State management (context, reducers)
├── queries/                 # React Query hooks for API calls
│   ├── mutations/
│   ├── queries/
├── styles/                  # Global styles and themes
└── utils/                   # Utility functions and helpers
```

---

## **Folder Details**

### 1. `components/`

#### Description:
This folder houses **purely presentational components** following the **Atomic Design methodology**. These components are **stateless** and reusable across the application. They rely entirely on props for rendering and do not include any business logic, API calls, or state management.

#### Structure:
```
components/
├── atoms/
│   ├── Button/
│   ├── TextInput/
│   ├── Icon/
├── molecules/
│   ├── FormField/
│   ├── Card/
├── organisms/
│   ├── LoginForm/
│   │   ├── LoginForm.tsx         # Stateless, presentational login form
│   │   ├── LoginForm.styles.ts   # Optional: Component-specific styles
│   ├── RegisterForm/
│   │   ├── RegisterForm.tsx      # Stateless, presentational registration form
│   │   ├── RegisterForm.styles.ts
├── templates/
│   ├── DashboardLayout/          # Layout combining organisms and templates
│   ├── MarketingPage/
```

#### Guidelines:
- **Atoms**: Represent the smallest, reusable UI components (e.g., buttons, inputs, icons).
- **Molecules**: Group atoms into functional components (e.g., input fields with labels, form sections).
- **Organisms**: Larger, reusable sections of the UI (e.g., forms, headers).
- **Templates**: High-level layouts that combine organisms and define page structure.

---

### 2. `containers/`

#### Description:
**Containers** manage state and logic. They act as an intermediary between presentational components and the application’s data layer (e.g., API calls, context). Containers handle:
- **Stateful logic** (e.g., form management, event handling).
- **Data fetching and mutations** (using React Query or custom hooks).
- **Event delegation**.

Containers should not render complex UI. They pass all required props and callbacks to presentational components.

#### Structure:
```
containers/
├── LoginFormContainer.tsx        # Manages state for LoginForm
├── RegisterFormContainer.tsx     # Manages state for RegisterForm
├── AvatarFormContainer.tsx       # Manages state for AvatarForm
```

---

### 3. `queries/`

#### Description:
This folder contains **React Query hooks** for data fetching and mutations. The logic here is **centralized** for reusability and consistency across the app.

#### Structure:
```
queries/
├── mutations/
│   ├── useLoginUser.ts           # Login mutation
│   ├── useRegisterUser.ts        # Registration mutation
├── queries/
│   ├── useFetchUser.ts           # Fetch user details
│   ├── useFetchSettings.ts       # Fetch app settings
```

#### Purpose:
- **Separation of concerns**: API logic remains outside components.
- Centralized location for all API interaction, enabling easier testing and updates.

---

### 4. `state/`

#### Description:
Global or local state management using React Context, reducers, or Zustand. This folder houses all logic unrelated to data fetching, such as UI state (e.g., modals, toasts).

#### Structure:
```
state/
├── toast/
│   ├── ToastContext.tsx          # Context for toast notifications
│   ├── toast.reducer.ts          # Reducer logic for managing toasts
├── user/
│   ├── UserContext.tsx           # Context for user authentication
│   ├── user.reducer.ts
```

---

### 5. `utils/`

#### Description:
Reusable utility functions, such as input validators, formatters, or helpers.

#### Structure:
```
utils/
├── validators.ts                 # Centralized validation logic
├── formatters.ts                 # Data formatting utilities
```

---

## **Best Practices**

### 1. **Keep Components Stateless**
- Presentational components in `components/` must:
  - Be reusable.
  - Avoid containing business logic or state.
  - Rely on props passed by containers.

---

### 2. **Use Containers for State Management**
- All application-specific logic resides in `containers/`.
- Containers connect:
  - React Query hooks (for API calls).
  - State management logic (via context or hooks).
  - Event handling and callback delegation.

---

### 3. **Leverage React Query for API Interaction**
- Define **queries** and **mutations** in the `queries/` folder.
- Ensure that components **do not make API calls directly**.
- Use hooks (e.g., `useMutation`, `useQuery`) in containers.

---

### 4. **Centralize Validation and Utilities**
- Use `utils/validators.ts` for input validation.
- Avoid spreading validation logic across components or containers.

---

### Example Integration: Login and Registration Forms

#### **LoginForm**

- A **stateless** component in `organisms/`.
- Renders the form UI, delegates all logic to the container.

#### **LoginFormContainer**

- Manages state for the `LoginForm`.
- Uses a custom `useLoginForm` hook to:
  - Handle input state and validation.
  - Use React Query for the `loginUser` mutation.
  - Delegate `onSubmit` and `onChange` handlers.

#### **useLoginForm**

- Centralized logic for login functionality.
- Isolates:
  - State (`useState` or `useReducer`).
  - Validation.
  - React Query integration (`useMutation`).

---

### Code Examples

#### **LoginForm.tsx**

```typescript
// Stateless component for login UI
import React from "react";
import TextInputGroup from "@/components/molecules/forms/TextInputGroup";
import ContainedButton from "@/components/atoms/buttons/ContainedButton";

const LoginForm = ({ formValues, formErrors, handleChange, handleSubmit, isPending }) => (
  <form onSubmit={handleSubmit}>
    <TextInputGroup
      label="Email"
      name="email"
      value={formValues.email}
      onChange={handleChange}
      error={!!formErrors.email}
      helperText={formErrors.email}
    />
    <TextInputGroup
      label="Password"
      name="password"
      value={formValues.password}
      onChange={handleChange}
      error={!!formErrors.password}
      helperText={formErrors.password}
    />
    <ContainedButton text="Login" type="submit" isLoading={isPending} />
  </form>
);

export default LoginForm;
```

#### **LoginFormContainer.tsx**

```typescript
import React from "react";
import LoginForm from "@/components/organisms/LoginForm";
import { useLoginForm } from "@/hooks/useLoginForm";

const LoginFormContainer = () => {
  const { formValues, formErrors, handleChange, handleSubmit, isPending } =
    useLoginForm();

  return (
    <LoginForm
      formValues={formValues}
      formErrors={formErrors}
      handleChange={handleChange}
      handleSubmit={handleSubmit}
      isPending={isPending}
    />
  );
};

export default LoginFormContainer;
```

#### **useLoginForm.ts**

```typescript
import { useState } from "react";
import { useMutation } from "@tanstack/react-query";
import { useLoginUser } from "@/queries/mutations/useLoginUser";

export const useLoginForm = () => {
  const [formValues, setFormValues] = useState({ email: "", password: "" });
  const [formErrors, setFormErrors] = useState({});
  const { mutate: loginUser, isLoading: isPending } = useLoginUser();

  const handleChange = (e) => {
    const { name, value } = e

.target;
    setFormValues({ ...formValues, [name]: value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    loginUser(formValues, {
      onSuccess: () => console.log("Login successful!"),
      onError: () => setFormErrors({ email: "Invalid login credentials" }),
    });
  };

  return { formValues, formErrors, handleChange, handleSubmit, isPending };
};
```


# Exp 13 - Simulate an Asynchronous Operation Using Promises in React
## NAME: BASHA VENU
## REG NO: 2305001005
## Aim
To develop a React application that simulates an asynchronous student-data operation using a JavaScript Promise, displays a loading message while the operation is in progress, and displays the result when the Promise is fulfilled.

## Objectives
- To understand the concept of a Promise in JavaScript.
- To create a Promise using `new Promise()`.
- To use `.then()` and `.catch()` to handle success and errors.
- To use React's `useState()` hook to manage application state.
- To display loading and result messages using conditional rendering.

## Program

### 1. App.jsx

```jsx
import { useState } from "react";
import "./App.css";

function fetchStudentData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const student = {
        name: "Arun",
        department: "CSE",
        year: "III"
      };

      resolve(student);

      // To test rejection:
      // reject(new Error("Unable to fetch student data"));
    }, 3000);
  });
}

function App() {
  const [loading, setLoading] = useState(false);
  const [student, setStudent] = useState(null);
  const [error, setError] = useState("");

  const handleFetch = () => {
    setLoading(true);
    setStudent(null);
    setError("");

    fetchStudentData()
      .then((data) => {
        setStudent(data);
      })
      .catch((err) => {
        setError(err.message);
      })
      .finally(() => {
        setLoading(false);
      });
  };

  return (
    <div className="app">
      <h1>Student Data Fetch</h1>

      <button onClick={handleFetch} disabled={loading}>
        {loading ? "Fetching..." : "Fetch Student"}
      </button>

      {loading && (
        <p>Fetching student information...</p>
      )}

      {student && (
        <div className="result">
          <h2>Student Details</h2>
          <p>Student Name: {student.name}</p>
          <p>Department: {student.department}</p>
          <p>Year: {student.year}</p>
          <h3>Status: Data Loaded Successfully</h3>
        </div>
      )}

      {error && (
        <p className="error">Error: {error}</p>
      )}
    </div>
  );
}

export default App;
```

### 2. App.css

```
.counter {
  font-size: 16px;
  padding: 5px 10px;
  border-radius: 5px;
  color: var(--accent);
  background: var(--accent-bg);
  border: 2px solid transparent;
  transition: border-color 0.3s;
  margin-bottom: 24px;

  &:hover {
    border-color: var(--accent-border);
  }
  &:focus-visible {
    outline: 2px solid var(--accent);
    outline-offset: 2px;
  }
}

.hero {
  position: relative;

  .base,
  .framework,
  .vite {
    inset-inline: 0;
    margin: 0 auto;
  }

  .base {
    width: 170px;
    position: relative;
    z-index: 0;
  }

  .framework,
  .vite {
    position: absolute;
  }

  .framework {
    z-index: 1;
    top: 34px;
    height: 28px;
    transform: perspective(2000px) rotateZ(300deg) rotateX(44deg) rotateY(39deg)
      scale(1.4);
  }

  .vite {
    z-index: 0;
    top: 107px;
    height: 26px;
    width: auto;
    transform: perspective(2000px) rotateZ(300deg) rotateX(40deg) rotateY(39deg)
      scale(0.8);
  }
}

#center {
  display: flex;
  flex-direction: column;
  gap: 25px;
  place-content: center;
  place-items: center;
  flex-grow: 1;

  @media (max-width: 1024px) {
    padding: 32px 20px 24px;
    gap: 18px;
  }
}

#next-steps {
  display: flex;
  border-top: 1px solid var(--border);
  text-align: left;

  & > div {
    flex: 1 1 0;
    padding: 32px;
    @media (max-width: 1024px) {
      padding: 24px 20px;
    }
  }

  .icon {
    margin-bottom: 16px;
    width: 22px;
    height: 22px;
  }

  @media (max-width: 1024px) {
    flex-direction: column;
    text-align: center;
  }
}

#docs {
  border-right: 1px solid var(--border);

  @media (max-width: 1024px) {
    border-right: none;
    border-bottom: 1px solid var(--border);
  }
}

#next-steps ul {
  list-style: none;
  padding: 0;
  display: flex;
  gap: 8px;
  margin: 32px 0 0;

  .logo {
    height: 18px;
  }

  a {
    color: var(--text-h);
    font-size: 16px;
    border-radius: 6px;
    background: var(--social-bg);
    display: flex;
    padding: 6px 12px;
    align-items: center;
    gap: 8px;
    text-decoration: none;
    transition: box-shadow 0.3s;

    &:hover {
      box-shadow: var(--shadow);
    }
    .button-icon {
      height: 18px;
      width: 18px;
    }
  }

  @media (max-width: 1024px) {
    margin-top: 20px;
    flex-wrap: wrap;
    justify-content: center;

    li {
      flex: 1 1 calc(50% - 8px);
    }

    a {
      width: 100%;
      justify-content: center;
      box-sizing: border-box;
    }
  }
}

#spacer {
  height: 88px;
  border-top: 1px solid var(--border);
  @media (max-width: 1024px) {
    height: 48px;
  }
}

.ticks {
  position: relative;
  width: 100%;

  &::before,
  &::after {
    content: '';
    position: absolute;
    top: -4.5px;
    border: 5px solid transparent;
  }

  &::before {
    left: 0;
    border-left-color: var(--border);
  }
  &::after {
    right: 0;
    border-right-color: var(--border);
  }
}

```

### 3. index.css

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f2f2f2;
}

h1 {
  color: darkblue;
}

h2 {
  color: darkgreen;
}
```

### 4. main.jsx

```
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)

```

## Output

### 1. Successful Student Data Fetch
<img width="1358" height="710" alt="image" src="https://github.com/user-attachments/assets/206c85c7-64d7-450d-8048-5a2ef0a7870f" />


### 2. Promise Rejection (Error Handling)
<img width="1085" height="575" alt="image" src="https://github.com/user-attachments/assets/7fab95e2-e39d-47de-b45a-bb25f000baeb" />


## Result
Thus, a React application was successfully developed to simulate an asynchronous student-data operation using JavaScript Promises. The application displayed a loading message and handled successful completion and errors using `.then()`, `.catch()`, and `.finally()`.

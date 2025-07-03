# 🌗 React Theme Blog Project - 전체 코드

---

## `/src/context/ThemeContext.js`

```javascript
import React, { createContext, useState } from "react";

export const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");
  const toggleTheme = () => setTheme(prev => (prev === "light" ? "dark" : "light"));

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

---

## `/src/components/NavBar.js`

```javascript
import React, { useContext } from "react";
import { Link } from "react-router-dom";
import { ThemeContext } from "../context/ThemeContext";

const NavBar = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);
  const navClass = theme === "light" ? "navbar navbar-light" : "navbar navbar-dark";

    return (
    <nav className={navClass}>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/blogs">Blogs</Link>
      <button onClick={toggleTheme}>
        Switch to {theme === "light" ? "Dark" : "Light"} Mode
      </button>
    </nav>
      );
};

export default NavBar;

```

---

## `/src/pages/BlogList.js`

```javascript
import { useEffect, useState } from "react";

const BlogList = () => {
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  
  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts?_limit=5")
      .then(res => res.json())
      .then(data => setPosts(data))
      .catch(err => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  
  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;

    return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
      );
};

export default BlogList;

```

---

## `/src/pages/Home.js`
```javascript
import React, { useContext } from "react";
import { ThemeContext } from "../context/ThemeContext";
const Home = () => {
  const { theme } = useContext(ThemeContext);
    return (
    <div>
      <h1>Welcome to the Blog!</h1>
      <p>Current Theme: {theme}</p>
    </div>
  );
  
export default Home;
```

---

## `/src/pages/About.js`
```javascript
import React from "react";

const About = () => {
    return (
    <div>
      <h2>About This Blog</h2>
      <p>This is a simple blog dashboard made with React.</p>
    </div>
      );
};
export default About;

```

---

## `/src/App.js`

```javascript
import React, { useContext } from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import NavBar from "./components/NavBar";
import Home from "./pages/Home";
import About from "./pages/About";
import BlogList from "./pages/BlogList";
import { ThemeContext } from "./context/ThemeContext";
import "./styles.css";

const App = () => {
  const { theme } = useContext(ThemeContext);

  const appStyle = {
    backgroundColor: theme === "light" ? "#ffffff" : "#222222",
    color: theme === "light" ? "#000000" : "#ffffff",
    minHeight: "100vh",
    padding: "1rem",
      };

  return (
    <div style={appStyle}>
      <BrowserRouter>
        <NavBar />
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/blogs" element={<BlogList />} />
        </Routes>
      </BrowserRouter>
    </div>
    );
};

export default App;
```

---

## `/src/index.js`

```javascript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { ThemeProvider } from "./context/ThemeContext";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <ThemeProvider>
    <App />
  </ThemeProvider>
);

```

---

## `/src/styles.css`

```css
.navbar {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  font-weight: bold;
}

.navbar-light {
  background-color: #eee;
}

.navbar-dark {
  background-color: #444;
}
.navbar a {
  text-decoration: none;
  color: inherit;
}
```
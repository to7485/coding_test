# 📄 React 메모 앱 소스코드

---

## `/src/pages/Notes.js`

```javascript
import React, { useEffect, useState } from "react";
import { getNotes, deleteNote } from "../utils/storage";

const Notes = () => {
  const [notes, setNotes] = useState([]);

  useEffect(() => {
    setNotes(getNotes());
  }, []);

  const handleDelete = (id) => {
    deleteNote(id);
    setNotes(getNotes());
  };

  return (
    <div>
      <h2>Your Notes</h2>
      {notes.length === 0 ? (
        <p>No notes yet</p>
      ) : (
        <ul>
          {notes.map(note => (
            <li key={note.id}>
              <strong>{note.title}</strong> - {note.content}
              <button onClick={() => handleDelete(note.id)}>Delete</button>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default Notes;
```

---

## `/src/pages/AddNote.js`

```javascript
import React, { useState } from "react";
import { useNavigate } from "react-router-dom";
import { saveNote } from "../utils/storage";

const AddNote = () => {
  const [title, setTitle] = useState("");
  const [content, setContent] = useState("");
  const navigate = useNavigate();

  const handleSubmit = (e) => {
    e.preventDefault();
    const newNote = {
      id: Date.now(),
      title,
      content
    };
    saveNote(newNote);
    navigate("/notes");
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>Add Note</h2>
      <input
        value={title}
        onChange={e => setTitle(e.target.value)}
        placeholder="Title"
        required
      />
      <textarea
        value={content}
        onChange={e => setContent(e.target.value)}
        placeholder="Content"
        required
      />
      <button type="submit">Save</button>
    </form>
  );
};

export default AddNote;
```

---

## `/src/components/NavBar.js`

```javascript
import React from "react";
import { Link } from "react-router-dom";

const NavBar = () => {
  return (
    <nav className="navbar">
      <Link to="/notes">Notes</Link>
      <Link to="/add">Add Note</Link>
    </nav>
  );
};

export default NavBar;
```

---

## `/src/App.js`

```javascript
import React from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import NavBar from "./components/NavBar";
import Notes from "./pages/Notes";
import AddNote from "./pages/AddNote";
import "./styles.css";

function App() {
  return (
    <BrowserRouter>
      <NavBar />
      <Routes>
        <Route path="/notes" element={<Notes />} />
        <Route path="/add" element={<AddNote />} />
        <Route path="*" element={<Notes />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

---

---

## `/src/utils/storage.js`

```javascript
// notes를 저장할 키
const STORAGE_KEY = "notes";

// localStorage에서 모든 메모를 불러오기
export const getNotes = () => {
  const stored = localStorage.getItem(STORAGE_KEY);
  try {
    return stored ? JSON.parse(stored) : [];
  } catch (e) {
    console.error("Failed to parse notes:", e);
    return [];
  }
};

// 메모 추가
export const saveNote = (note) => {
  const notes = getNotes();
  notes.push(note);
  localStorage.setItem(STORAGE_KEY, JSON.stringify(notes));
};

// 메모 삭제
export const deleteNote = (id) => {
  const notes = getNotes();
  const updatedNotes = notes.filter(note => note.id !== id);
  localStorage.setItem(STORAGE_KEY, JSON.stringify(updatedNotes));
};
```


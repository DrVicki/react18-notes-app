# react18-notes-app
Create a PWA with React Version 18

In this lesson, we will be building a simple note-taking app with React JS and then making it a Progressive Web App.

## Creating the project

We will use React 18 (the latest version of React JS) to build this project. Remember, we need to have Node version 14.0.0 (or higher) and npm version 5.6 or more to use React 18.

```
npx create-react-app notes
```
And then we have our react notes app load.

After it is installed, we will run:

```
cd notes
npm start
```
After this, we open our newly created react app on our favorite code editor,

## Creating the Page

And now, we will create our `homepage` with contain our App component. In the `index.js`, we have:

```
import React from "react";
import App from "./App";
import { createRoot } from "react-dom/client";
const container = document.getElementById("root");
const root = createRoot(container);
root.render(<App />);
```

And in our `App.js` we have

```
import React, { useState } from 'react';
import './style.css';
export default function App() {
  return (
    <div>
      <h1>My Notes</h1>
      <input type="text" />
      <button>Save</button>
    </div>
  );
}
```

And now we have this displayed on our page:

First version of the page

## Creating the Notes Component

We will create a `Notes` component that will display any available notes. The component will be inside a folder, and the folder will be created inside the `src` folder and called `components`.

After that, we will create a file called `Notes.js` inside the `components` folder and create a simple function that loops through available data served in the props, creating different p elements.

Component file structure

Inside the `Notes.js` file, we have:

```
import React from 'react';
function Notes({ data }) {
  return data.map((value) => <p>{value}</p>);
}
export default Notes;
```
Our Notes component will always take the parameter data. Now to import it into our `App.js`, we have:

```
import React, { useState } from 'react';
import Notes from './components/Notes';
import './style.css';
export default function App() {
  return (
    <div>
      <h1>My Notes</h1>
      <input type="text" />
      <button>Save</button>
      <Notes/>
    </div>
  );
}
```

Remember, our `Notes` component needs parameter data. We will create states for the data that will update whenever the save button is clicked.

```
import React, { useState } from 'react';
import Notes from './components/Note';
import './style.css';
export default function App() {
  let [list, setList] = useState([]);
  let [newNote, setNewNote] = useState('');
  function addNote() {
    let addedNote = list.concat(newNote);
    setList(addedNote);
    setNewNote('');
  }
  function handleChange(e) {
    setNewNote(e.target.value);
  }
  return (
    <div>
      <h1>My Notes</h1>
      <input type="text" value={newNote} onChange={handleChange} />
      <button onClick={addNote}>Save</button>
      <Notes data={list} />
    </div>
  );
}
```
And now, we should be able to save some notes with our app.

The app, working

## Registering our Service Worker

What is a service worker? A service worker is just a required JS program for our app to be a Progressive Web App.

So, to use a service worker, we will have to register it on our `index.js`, so we import `serviceWorker.js` into our `index.js`.

**index.js**:

```
import React from "react";
import App from "./App";
import * as serviceWorker from "./serviceWorker"
import { createRoot } from 'react-dom/client';
const container = document.getElementById('root');
const root = createRoot(container);
root.render(<App/>);
serviceWorker.register():
```

## Editing our `manifest.json` file

The final step to making our app a PWA is to change some things in our `manifest.json` file. We will set our icons and other options available.

```
{
  "short_name": "My Notes App",
  "name": "Notes Progressive Web Application",
  "icons": [
    {
      "src": "icon.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icon.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ],
  "start_url": "./",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}
```
And finally, we have a PWA app working that can run on any device like a native app.



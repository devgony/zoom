# Noom

Zoom Clone using NodeJs, WebRTC and Websockets

# #0.2 Server Setup (07:17)

```
npm i nodemon -D
git init
npm i @babel/core @babel/cli @babel/node @babel/preset-env -D
npm i express pug
touch babel.config.json nodemon.json src/server.js
```

```json
// babel.config.json
{
  "presets": ["@babel/preset-env"]
}

// nodemon.json
{
  "exec": "babel-node src/server.js"
}

// package.json
"scripts": {
    "dev": "nodemon"
},
```

```js
// src/server.js
import express from "express";

const app = express();
app.set("view engine", "pug");
app.set("views", __dirname + "/views");
app.use("/public", express.static(__dirname + "/public"));
app.get("/", (req, res) => res.render("home"));
app.get("/*", (req, res) => res.redirect("/"));

const handleListen = () => console.log(`Listening on http://localhost:3000`);
app.listen(3000, handleListen);
```

# #0.3 Frontend Setup (08:53)

```
mkdir -p src/public/js src/views
touch src/public/js/app.js src/views/home.pug
```

## don't need to restart nodemon for frontend (src/public/)

- but static files in views need to be restarted

```json
// nodemon.json
{
  "ignore": ["src/public/*"],
  "exec": "babel-node src/server.js"
}
```

## MVP.CSS

- add `https://unpkg.com/mvp.css`

```pug
//- src/views/home.pug
doctype html
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(http-equiv="X-UA-Compatible", content="IE=edge")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        title Noom
        link(rel="stylesheet", href="https://unpkg.com/mvp.css")
    body
        header
            h1 Noom
        main
            h2 Welcome to Noom
        script(src="/public/js/app.js")
```

# #0.4 Recap (04:09)

# #1.0 Introduction (02:14)

## http protocal

- https is `stateless`: server forgets who you are
- 1 request : 1 response

## websocket protocal

1. ws request and accpet handshake (connection)
2. send bi-directional message
3. close connection

- Can work between two backend server as well.

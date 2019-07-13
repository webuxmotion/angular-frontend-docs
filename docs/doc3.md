---
id: doc3
title: Running setup
---
1. Edit **package.json** in folder /nodejs-backend
```
...
"scripts": {
    "start": "node index",
    "server": "nodemon index",
    "test": "echo \"Error: no test specified\" && exit 1",
    "client-install": "npm install --prefix client",
    "client": "npm run start --prefix client",
    "dev": "concurrently \"npm run server\" \"npm run client\""
},
...
```

2. Install concurrently in folder /nodejs-backend
```
npm i -D concurrently
```

3. Run backend and frontend
```
npm run dev
```

4. Edit file /client/src/app/app.component.html
```
<h1>Working</h1>
```

5. Check frontend in browser [http://localhost:4200/](http://localhost:4200/)

6. Check backend in browser [http://localhost:5000/](http://localhost:5000/)

See message
```
Cannot GET /
```
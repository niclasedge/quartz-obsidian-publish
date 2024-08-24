---
title: Create Electron Apps
description: How to create an App that runs on win, macos and Linux at the same time
authors: niclasedge
images: null
tags:
- AI
toc_max_heading_level: 5
created: 26.07.2024
---
I'd be happy to help you set up an Electron app using Electron Forge. Electron Forge is a powerful tool that simplifies the process of creating, packaging, and distributing Electron applications. Let's go through the steps to set up a basic Electron app:

1. First, make sure you have Node.js installed on your system. If not, download and install it from nodejs.org.

2. Open a terminal or command prompt and create a new directory for your project:

```bash
mkdir my-electron-app
cd my-electron-app
```

3. Initialize a new Node.js project:

```bash
npm init -y
```

4. Install Electron Forge as a dev dependency:

```bash
npm install --save-dev @electron-forge/cli
```

5. Initialize your project with Electron Forge:

```bash
npx electron-forge import
```

This command will add several dependencies and create some boilerplate files for your Electron app.

6. Now, let's create a basic Electron app. Open the `src/index.js` file (created by Electron Forge) and replace its contents with the following code:



```javascript
const { app, BrowserWindow } = require('electron');
const path = require('path');

// Handle creating/removing shortcuts on Windows when installing/uninstalling.
if (require('electron-squirrel-startup')) {
  app.quit();
}

const createWindow = () => {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false,
    },
  });

  // Load the index.html of the app.
  mainWindow.loadFile(path.join(__dirname, 'index.html'));

  // Open the DevTools.
  // mainWindow.webContents.openDevTools();
};

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow);

// Quit when all windows are closed, except on macOS.
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

app.on('activate', () => {
  // On OS X it's common to re-create a window in the app when the
  // dock icon is clicked and there are no other windows open.
  if (BrowserWindow.getAllWindows().length === 0) {
    createWindow();
  }
});

```

7. Create an `index.html` file in the `src` directory:



```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello Electron!</title>
    <meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline';" />
  </head>
  <body>
    <h1>Hello Electron!</h1>
    <p>Welcome to your Electron application.</p>
  </body>
</html>

```

8. Your project structure should now look like this:

```
my-electron-app/
├── package.json
├── src/
│   ├── index.js
│   └── index.html
└── ...
```

9. To start your Electron app, run:

```bash
npm start
```

This will launch your Electron application.

10. To package your app for distribution, you can use the following command:

```bash
npm run make
```

This will create distributable packages for your application in the `out` folder.

That's it! You now have a basic Electron app set up using Electron Forge. You can continue to build your app by modifying the `src/index.js` and `src/index.html` files, and adding more functionality as needed.

Would you like me to explain any part of the setup process or the code in more detail?
# Quasagram

## Install app dependencies
```bash
npm install
```

## Install backend dependencies
```bash
cd backend
npm install
```

## Add your Heroku project name
- On line 8 of `/backend/package.json` add your own Heroku project name 
```
{
  ...
  "scripts": {
    ...
    "deploy": "heroku builds:create -a [YOUR HEROKU PROJECT NAME]"
  },
  ...
}
```

## Add your own **serviceAccountKey.json** file
- Ensure you have a Firebase Project named Quasagram
- On the Firebase website, on the Project Overview page, add a new web app (if you've not already added one).
- Once created, click on **1 App** > **Cog icon** > **Service accounts**.
- Generate a new private key, store it in your `/backend` folder
- Rename the private key to `serviceAccountKey.json`

## Add your Production API URL
- On line 10 of `/quasar.conf.js` add your own Production API URL (with no slash at the end) e.g. 'https://your-project-name.herokuapp.com'
```
API_PRODUCTION = '[YOUR LIVE BACKEND URL]'
```

## Add your Firebase Storage Bucket URL
- On line 28 of `/backend/index.js` add your own Firebase Storage Bucket URL. You can get this from the Firebase Console e.g. "quasagram-1hg13.appspot.com"
```
admin.initializeApp({
  ...
  storageBucket: "[YOUR FIREBASE STORAGE BUCKET URL]"
});
```

## Add your Public & Private Vapid Keys
- If you haven't already, generate some vapid keys and store these in a text file outside of your project:
```
cd backend
npm run web-push generate-vapid-keys
```
- `/backend/index.js` - add your public & private keys to lines 41 & 42
- `/src/pages/PageHome.vue` - add your public key to line 263

## Start the backend (from /backend folder)
```bash
npm start
```

## Start the app in PWA development mode (from / folder)
```bash
quasar dev -m pwa
```

**Note:** You may need to clear site data and reload:
- Chrome Dev Tools
- Application > Clear storage > Clear site data
- Reload the app

## Deploy Your Backend to Heroku

- Create a Heroku project (if you've not already):
- **Heroku Website** > **Dashboard** > **New** > **Create new app**
- Give it a name, e.g. **quasagram-backend**
- Click **Create app**
- Deploy the backend:
```
cd backend
```
```
heroku builds:create -a YOUR_HEROKU_APP_NAME
```
OR just run our shortcut script (make sure you add your Heroku project name to `/backend/package.json` first):
```
npm run deploy
```
- Copy your Heroku app URL from the terminal when deployed
- Add your Heroku app URL to line 10 on `quasar.conf.js` (**DON'T** include the final slash):
e.g.
```
let API_PRODUCTION = 'https://your-heroku-project-name.herokuapp.com'
```
- Remember to switch to your Production API URL on line 50 of `quasar.conf.js`:
```json
build: {
  env: {
    API: API_PRODUCTION // API_LOCAL | API_PRODUCTION
  },
  ...
}
```

## Build and Deploy Your Quasar App to Firebase

- From your project root:
```
quasar build -m pwa
```
- Install Firebase CLI globally and login (if you've not already):
```
npm install -g firebase-tools
firebase login
```
- Initialize Firebase Hosting:
```
firebase init
```
- Choose **Hosting**
- Choose **Use an existing project**
- Choose the **Quasagram** project you created on Firebase
- Use these options:
  - What do you want to use as your public directory?: **dist/pwa**
  - Configure as a single-page app?: **No**
  - File dist/pwa/index.html already exists. Overwrite?: **No**
- Deploy the app:
```
firebase deploy
```
- Copy the **Hosting URL** from the terminal and launch on any Desktop / Mobile browser
- Or you can use our shortcut script to build and deploy:
```
npm run deploy
```

## To generate icons
- Install Icon Genie CLI globally
```
npm install -g @quasar/icongenie
```
- Generate the icons
```
npm run icons
```
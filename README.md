## Deployment with Vercel (Zeit.now)

In order to deploy our React apps with vercel we need two things:
- a vercel account
- the Vercel CLI to make deployments of our app from the terminal

We can also deploy NodeJS / Express APIs with Vercel (instructions on this are also in this guide)

### Setup: Account creation & CLI installation

- Signup: vercel.com/signup
  - Use GitHub for signup
  - In case you are not logged in - log into GitHub

- After account creation
  - Go to tab "Settings" &gt; Email
    - this Email (=your GitHub email) will be used for login
  - Direct link to settings: https://vercel.com/account

- Install vercel: `npm i -g vercel`
  - If installing a global package gives you an error, try with sudo:
  - `sudo npm i -g vercel`

- Login (just on first usage)
  - In terminal type: `vercel login`
  - State your email address you got from Vercel settings page
  - hit enter and - important - don't close the terminal, keep it open!!
  - You will now get an email for verifying your account
  - Once you clicked the confirm link in the email and get the verification
    - go back to the terminal
    - you should get a message for successful connection

DONE!

You only need to do this terminal login once (it will last for a while until you get prompted again)


### Deployment

#### Frontend

- Get into a folder with a react app that you want to deploy
- Type `vercel`
- Follow the instructions (in case of doubt - accept all the defaults please with enter please)

##### Special handling of first deployment

- on first deployment you likely will receive an error.... here's why :)
  - Vercel - as of now - treats React warnings as errors. and will cancel the build on warnings!
  - very likely you WILL have some React warnings in your app, e.g. due to not used variables, etc
  - you can see the concrete issue when you run "vercel logs <yourAppName>"
  - it will tell you that you need to set the environment variable "CI" to false, to allow depeloyment of a React app that has unfixed warnings

- the fix: go to the vercel dashboard: https://vercel.com/dashboard
  - click the title of your app (should be listed at the first one in the list)
  - click the tab "Settings"
  - in the left menu: go to section "Environment variables"
  - set a "Plaintext" variable
    - In the Name field put the value: CI
    - In the Value field put the value: false
    - Make the variable available in all environments
    - Click save
  - Now try to redeploy the app, with: `vercel --prod`
    - Now hopefully the build will run through!

##### Open & update deployed page

- After deployment finished you receive two links
  - Open the "Production" link in the browser
  - Check if your App was deployed correctly
  - The other link "Inspect" is for checking your deployment status & any issues

- On all subsequent deployments you do `vercel --prod`
  - if you just type "vercel" you get a preview deloyment
    ( to check out if everythings works okay - before you overwrite your real webpage)


#### Backend

Get into the folder of a express app that you want to deploy

Add a file "vercel.json" at the top level of the folder

Put in the following content:

```
{
  "version": 2,
  "builds": [
      { "use": "@vercel/node", "src": "app.js" }
  ],
  "routes": [
      { 
        "src": "/(.*)", 
        "dest": "app.js"
      }
    ]
}
```

Replace "app.js" with the name of your app startup file (e.g. "server.js" or "index.js", whatever you use in your app). Be aware "app.js" is stated TWO times in the file, so please replace both occurences. Otherwise it will not work

Deployment process: 

- Type `vercel`
- Follow the instructions (in case of doubt - accept all the defaults please with enter please)

- After deployment finished you receive two links
  - Open the "Production" link in the browser
  - Check if your App was deployed correctly
  - The other link "Inspect" is for checking your deployment status & any issues

- On all subsequent deployments you do `vercel --prod`
  - if you just type "vercel" you get a preview deloyment
    ( to check out if everythings works okay - before you overwrite your real webpage)

##### Caution - Backend Limitations

Vercel has currently (Feb 2021) the limitations, that you cannot write / upload files to the filesystem

Also there is no support for websockets.

In case you wanna either deploy apps with file upload or messaging featurs, rather use Heroku as free alternative for hosting node JS:

https://github.com/losrobbos/heroku-node-deploy-guide

However: For normal, simple express backends that do not write files or just forward files to a file provider for storage (e.g. AWS S3) you can stick with Vercel. It is very easy to setup and the performance of deployed APIs is typically quite good.

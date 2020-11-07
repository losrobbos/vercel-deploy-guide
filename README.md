## Setup Deployment with Vercel (Zeit.now)

- Signup: vercel.com/signup
  - Use GitHub for signup
  - In case you are not logged in - log into GitHub

- After account creation
  - Go to tab "Settings" &gt; Email
    - this Email (=your GitHub email) will be used for login
  - Direct link to settings: https://vercel.com/account

- Install vercel: `npm i -g vercel`
	- If installing a global package gives you and error, try with sudo:
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

You only need to do this terminal login once (it will last for several days)


### Deployment test

#### Frontend

- Get into a folder with a react app that you want to deploy
- Type `vercel`
- Follow the instructions (in case of doubt - accept all the defaults please with enter please)

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

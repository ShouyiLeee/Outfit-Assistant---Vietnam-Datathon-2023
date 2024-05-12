# quickstart-web-npm-js
## Note: I already add list product template into the web UI
## Setup license key
1. Go to https://developer.deepar.ai
2. Sign up
3. Create a project and a Web app
4. Copy the license key
5. Paste it into `src/index.js` (replace `your_license_key_goes_here`)

## Test locally
- Open the terminal in the root of the project
- Run `npm install`

## Test on desktop
- Run `npm run dev`
- If the browser doesn't open automatically, open http://localhost:8888

Make sure to use external webcam to be able to test feet tracking properly.
Or better yet, test on mobile.

## Test on mobile
To test on mobile we need to setup a local server that can be accessed via https on the mobile browsers.
For that we will use [Ngrok](https://ngrok.com/).

### 1. Ngrok Setup
For Ngrok setup, the first thing you need is to go to the [Ngrok website](https://ngrok.com/)
and sign in. After you sign in into Ngrok go to [Ngrok Dashboard](https://dashboard.ngrok.com/login) and 
follow the steps to download the ngrok installation file.

### 2. Ngrok tunnel
Open a new terminal and run the Ngrok HTTP tunnel on port 8888.
```shell
ngrok http 8888
```
Now you should have Ngrok running and a https URL listed in your terminal.
Copy the URL (except for the "https://" part) for the next step.

### 3. Project setup
In order for DeepAR web app to work it needs a license key that is connected to the website domain.
We will create a free license key for the Ngrok domain just for testing purposes.

1. Go to DeepAR developer [projects](https://developer.deepar.ai/projects) page and click `+ NEW PROJECT`.
2. Give it a name and choose a free tier.
3. Under the "Web app" click `+ ADD APP`
4. Paste the Ngrok domain from the terminal. Something like '7940-188-252-198-101.eu.ngrok.io'. Remember NOT to copy the "https://" part.
5. Click `COPY SDK KEY` and paste it in the `src/index.js` in place of 'your_license_key_goes_here'.

### 3. Run the web app
Now we need to run a local server. For that we are goin to use a simple python http server.
From our experiance, webpack dev server doesn't work well with Ngrok.
Make sure to use the web app on one client only, since python server cannot serve multiple clients.
That means that you cannot have it open in multiple tabs or that it cannot be running on desktop and mobile browser at the same time.

Open a new terminal (don't close the one with Ngrok running) build the web app.
```shell
npm run build
```

Now run the local server on port 8888 in the `dist` directory.
```shell
cd dist
python -mhttp.server 8888 
```
This should now be serving your web app from the local server.

### Run the web app on mobile

1. Copy the https URL from the Ngrok terminal, something like 'https://7940-188-252-198-101.eu.ngrok.io'.
2. Generate a QR code from the URL, you can use https://qr.io/.
3. Scan the QR code on your mobile and test the web app.

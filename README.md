The idea is the user signs in with their spotify account and agrees to share their data with this backend application as long as their are logged in.
If sucessful the user is redirected to the client application with the applications valid access_token in the url. Its then the front-end applications
job to parse this valid access_token from url and make api calls to spotify. 


# SETUP BACKEND 
##  Development On Local Environment

server.js has hardcoded that this backend server is on port 8888, and the frontend application is on port 3000



Download this Folder and go into it. On the terminal run:

```
 npm install
```
Register for a Spotify Application here: 
https://developer.spotify.com/dashboard/applications


Click on the edit settings button


Under the section Redirect URIs add
http://localhost:8888/callback 
as a callback url. 

Then scroll down and click Save.

For the command below: 
Replace XXXX with Client ID, and Replace YYYY with Client Secret, which you get from https://developer.spotify.com/dashboard/applications

```
export SPOTIFY_CLIENT_ID=XXXX
export SPOTIFY_CLIENT_SECRET=YYYY
npm start
```

Then go to http://localhost:8888/login in your browser. 
This will ask the user to login.

It will then redirect to your front end application (I'm using an React app on port 3000)
http://localhost:3000?access_token=ZZZZZ
where ZZZZZ is a valid access token that your front-end application uses

##  Deploy on Heroku
Download the Heroku Command Line Tools (CLT)
Go to this folder in terminal

Run these commands but:
Replace mybackend with what you want to call this application
Replace abc123 with Client ID
Replace cba456 with Client Secret
Replace https://mybackend.herokuapp.com/callback with the backend url (just replace mybackend like above)
Repalce https://myfrontend.herokuapp.com with the front application you have deployed on Heroku  (I deployed my React app on Heroku)
```
heroku create mybackend
heroku config:set SPOTIFY_CLIENT_ID=abc123
heroku config:set SPOTIFY_CLIENT_SECRET=cba456
heroku config:set REDIRECT_URI=https://mybackend.herokuapp.com/callback
heroku config:set FRONTEND_URI=https://myfrontend.herokuapp.com
git push heroku master
```
Then go to 
https://developer.spotify.com/dashboard/applications


Click on the edit settings button


Under the section Redirect URIs add
https://mybackend.herokuapp.com/callback
as a callback url. 


Then scroll down and click Save.

You should now be able to go to http://mybackend.herokuapp.com/login and it will eventually redirect to http://myfrontend.herokuapp.com?access_token=ZZZZZwhere ZZZZZ is a valid access token that you can use to do operations in the Spotify API.

---
post_title: Obtaining Google OAuth2 Tokens
nav_title: Obtaining Google OAuth2 Tokens
---

Set up your API project and enable the Google Analytics Reporting Api. 

Log in to https://console.developers.google.com/ to get started. 

At the top of the dashboard click the "Enable API" button. 

![google-oauth2-tokens1](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens1.png)

In the search box, look for the API you want to enable. In this instance, we are looking for the Google Analytics Reporting API. Click on it. 

![google-oauth2-tokens2](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens2.png)

Click the "Enable" button at the top.

![google-oauth2-tokens3](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens3.png)

On the side bar, click "Credentials." 

Click on the "Create Credentials" drop dow, and select "OAuth Client ID."

![google-oauth2-tokens4](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens4.png)

Select "Web Application." 
Create a unique name for your project.  You'll also need to provide a redirect URL, which can be any page that isn't a Public IP address (i.e. https://www.google.com/). 
Choose "Create."

![google-oauth2-tokens5](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens5.png)

Click on your newly created credentials. 

![google-oauth2-tokens6](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens6.png)

At the top, choose "Download JSON." 

![google-oauth2-tokens7](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens7.png)

For the next step, we're going to use the OAuth 2 gen script and the JSON we just downloaded to generate our tokens. We've created a Google Token Fetcher with everything you need.

Clone [this repo](https://github.com/astronomerio/google-token-getter). Inside the `index.js`, provide your `CLIENT_ID`, `CLIENT_SECRET`, and `REDIRECT_URL`, which can be found in the JSON file you just downloaded.

```
var GoogleAuth = require('google-auth-library');
var readline = require('readline');
var auth = new GoogleAuth();

// Provide your Client ID, Client Secret, and Redirect URL below
var oauth2Client = new auth.OAuth2('CLIENT_ID','CLIENT_SECRET', 'REDIRECT_URL')

getNewToken(oauth2Client);

// Special Note: Change the end of the scope url to the api you are generating it for (if not Google Analytics) 
function getNewToken(oauth2Client) {
    const authUrl = oauth2Client.generateAuthUrl({
        access_type: 'offline',
        scope: ['https://www.googleapis.com/auth/analytics.readonly']
    });
    console.log('Authorize this app by visiting this url: ', authUrl);
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout,
    });

    rl.question('Enter the code from that page here: ', (code) => {
        rl.close();
        oauth2Client.getToken(code, (err, token) => {
            if (err) {
                console.log('Error while trying to retrieve access token', err);
                return;
            }
            oauth2Client.credentials = token;
            console.log(token);
        });
    });
}
```

Save your changes in `index.js`.  
From inside your cloned folder, `npm run dev`. The script will install dependencies and run. You should receive a URL in the terminal output.  Copy that URL and paste it into your browser.

The page will prompt you to log in with a Google account and authorize the app. 

Once you have done that, you will be redirected to your Redirect URL. From the address bar, in copy everything after the equals sign, and paste it into your terminal input.

![google-oauth2-tokens9](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens9.png)

Hit enter.

![google-oauth2-tokens10](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens10.png)

Your tokens will be output to the console. 

```
{
    "access_token" : "access-token", 
    "refresh_token" : "refresh-token", 
    "token_type" : "Bearer", 
    "expiry_date" : 1234567890
}
```

![google-oauth2-tokens11](/1.0/assets/img/guides/google-oauth/google-oauth2-tokens11.png)





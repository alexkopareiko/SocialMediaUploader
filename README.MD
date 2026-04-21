# YouTube Upload App

This app lets you sign in with your Google account and upload videos to your YouTube channel from Windows.

If this app helps you and you want to support development, you can support me here:

[Support me on Ko-fi](https://ko-fi.com/nikfortgames)

## What you need

Before using the app, you need:

- A Google account that owns or manages a YouTube channel
- A Google Cloud project
- The `YouTube Data API v3` enabled in that project
- An OAuth `Client ID` and `Client Secret` for a desktop app

Important:

- Do **not** use a service account. YouTube uploads do not work with service accounts.
- Your `Client Secret` is sensitive. Treat it like a password.
- The app uses OAuth, so the first sign-in opens a browser window for Google authorization.

## How to get a Client ID and Client Secret

### 1. Create a Google Cloud project

1. Open Google Cloud Console: https://console.cloud.google.com/
2. Create a new project, or select an existing one.

### 2. Enable the YouTube Data API

1. In Google Cloud Console, open `APIs & Services`.
2. Go to `Library`.
3. Search for `YouTube Data API v3`.
4. Click it and press `Enable`.

### 3. Configure the OAuth consent screen

1. In Google Cloud Console, open `APIs & Services` > `OAuth consent screen`.
2. Choose the appropriate user type for your case.
3. Fill in the basic app information.
4. Add your email address as a developer/contact email.
5. Save the setup.

Notes:

- If your app is in testing mode, only test users you add can log in.
- If Google asks for scopes during setup, the app will request YouTube access during sign-in.

### 4. Create desktop OAuth credentials

1. Open `APIs & Services` > `Credentials`.
2. Click `Create Credentials`.
3. Choose `OAuth client ID`.
4. For application type, select `Desktop app`.
5. Give it a name.
6. Click `Create`.

Google will show:

- `Client ID`
- `Client Secret`

Copy both values.

## How to enter the credentials in the app

Open the app and paste these values into:

- `YouTube Client ID`
- `YouTube Client Secret`

Then save them.

Example format:

- Client ID: `1234567890-abc123def456.apps.googleusercontent.com`
- Client Secret: `GOCSPX-xxxxxxxxxxxxxxxx`

The app can also read them from environment variables:

- `YOUTUBE_CLIENT_ID`
- `YOUTUBE_CLIENT_SECRET`

## First login

When you log in for the first time:

1. The app opens your browser.
2. You sign in to Google.
3. Google asks you to allow access to your YouTube account.
4. After approval, the app stores the OAuth session locally so you do not need to sign in every time.

## Where the app stores data

The app stores local configuration in your Windows profile under `AppData\Roaming\YouTubeUpload`.

This includes:

- saved YouTube OAuth client settings
- local OAuth session/token data
- queue/app data used by the app

If you move to another PC, you will usually need to sign in again.

## Security notes

- Anyone with your `Client Secret` can use your OAuth app configuration.
- Anyone with access to your local Windows account may be able to access locally stored app data.
- If you think your credentials were exposed, rotate them in Google Cloud and create a new OAuth client.

## Troubleshooting

### “Enter and save your YouTube OAuth Client ID and Client Secret before logging in.”

You have not entered valid OAuth credentials yet. Double-check both values and save them again.

### Google says the app is unverified

This can happen if your OAuth consent screen is still in testing or not fully configured. Add your Google account as a test user if needed.

### Login works, but uploads fail

Check:

- the selected Google account actually has a YouTube channel
- `YouTube Data API v3` is enabled
- the project has quota available
- you approved the requested YouTube permissions

### Wrong Google account opened in browser

Sign out of the wrong Google account in the browser, or use a private/incognito window, then try again.

## Good practice

- Use a dedicated Google Cloud project for this app
- Keep the `Client Secret` private
- Start with a test channel/account before using a production one
- If multiple people will use the app, give each trusted setup its own OAuth client/project

## Official Google references

- YouTube API credentials overview: https://developers.google.com/youtube/registering_an_application
- OAuth for installed apps: https://developers.google.com/youtube/v3/guides/auth/installed-apps
- YouTube authorization overview: https://developers.google.com/youtube/v3/guides/authentication

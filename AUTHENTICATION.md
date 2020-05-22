# Authentication

To use oAuth you need to configure environment variables with ID and secret and configure the service accordingly.

This project comes pre-configured to handle Facebook, Google and Twitter oAuth if you provide the ID and sercret for the service via environment variables.

You can pass them on the command line or put them in `.env` file which will be loaded at startup (see [.env.default](https://github.com/iaincollins/nextjs-starter/blob/master/.env.default) for an example).

If you want to add new oAuth providers (such as GitHub), you will need to:

- Add the oauth provider configuration in next-auth.providers.js
- Add a field to your User model (in 'index.js') with the name of the provider
- Configure the service to point to your website (as in the examples below)
- Specify the environment variables at run time

## Configuring your account

These guides are approximate as exactly how to configure oAuth varies for each provider and tends to change when they update their developer portals, which can be quite often. If you can't see the options mentioned, try exploring the UI in the developer portal or configuration pages.

Due to the volume of requests I'm not usually able to help with specific problems but pull requests with improved or extended instructions are very welcome.

Tip: Twitter's oAuth implementation is the most permissive and easiest to configure, you may want to start with it. If you run into problems, you might
want to check email sign-in is working as baseline.

Please note that Facebook oAuth cannot be used to sign in to 'localhost' and that if you want to sign in to `localhost` with Google+ you must specifically add something like `http://localhost:3000/auth/oauth/google/callback` as a authorized redirect URI for your application.

### Facebook Login

Environment variables:

- FACEBOOK_ID
- FACEBOOK_SECRET

Configuration steps:

1. Go to [Facebook Developers](https://developers.facebook.com/)
2. Click **Apps > Create a New App** in the navigation bar
3. Enter _Display Name_, then choose a category, then click **Create app**
4. Specify _App ID_ as the **FACEBOOK_ID** Config Variable
5. Specify _App Secret_ as the **FACEBOOK_SECRET** Config Variable
6. Click on _Settings_ on the sidebar, then click **+ Add Platform**
7. Select **Website**
8. Enable 'Client OAuth Login' and 'Web OAuth Login'
9. list`http://your-server.example.com/auth/oauth/facebook/callback` under 'Valid OAuth redirect URIs'
10. List your sites domain under 'domains'

### Google+

Environment variables:

- GOOGLE_ID
- GOOGLE_SECRET

Configuration steps:

1. Visit [Google Cloud Console](https://cloud.google.com/console/project)
2. Click the **CREATE PROJECT** button, enter a _Project Name_ and click **CREATE**
3. Then select _APIs_ then _Credentials_
4. Select **Create new oAuth Client ID** and enter the following:

- **Application Type**: Web Application
- **Authorized Javascript origins**: `http://your-server.example.com/`
- **Authorized redirect URI**: `http://your-server.example.com/auth/oauth/google/callback`

5. Specify _Client ID_ as the **GOOGLE_ID** Config Variable
6. Specify _Client Secret_ as the **GOOGLE_SECRET** Config Variable
7. Enable Google+ on the project - if you don't, sign in with Google+ will fail!

### Twitter

Environment variables:

- TWITTER_KEY
- TWITTER_SECRET

Configuration steps:

1. Sign in at [https://apps.twitter.com](https://apps.twitter.com)
2. Click **Create a new application**
3. Enter your application name, website and description
4. For **Callback URL**: `http://your-server.example.com/auth/oauth/twitter/callback`
5. Go to **Settings** tab
6. Under _Application Type_ select **Read and Write** access
7. Check the box **Allow this application to be used to Sign in with Twitter**
8. Click **Update this Twitter's applications settings**
9. Specify _Consumer Key_ as the **TWITTER_KEY** Config Variable
10. Specify _Consumer Secret_ as the **TWITTER_SECRET** Config Variable

# Posting to Instagram straight from your PC

Kestrel can post Reels through Meta's own API instead of going via Upload-Post. It is free, there is no
middleman, and because it uses the official API rather than a browser pretending to be you, there is no
ban risk.

The catch is that Meta makes you create a developer app to get a token. It is about fifteen minutes of
clicking, once. **Most people should just use Upload-Post** — this is for people who would rather not pay
a second subscription, or who want their footage to touch nothing but their own machine and Meta.

## What you need before you start

| | |
|---|---|
| An Instagram **Professional** account | Creator or Business, both work. Free to switch in the Instagram app: Settings → Account type |
| A **Facebook Page** linked to it | Also free. Instagram's API will not talk to a personal profile |
| A Meta developer account | developers.facebook.com, free |

## What Kestrel needs at the end

Three values, which go into Settings → Publishing → Advanced:

- **Meta App ID** and **App Secret** — from your app's dashboard
- **A user access token** with these four permissions:
  `instagram_basic`, `instagram_content_publish`, `pages_show_list`, `pages_read_engagement`

You paste a short-lived token. Kestrel exchanges it for a long-lived Page token that does not expire, so
this is genuinely a one-time setup.

## The steps

1. **developers.facebook.com** → My Apps → Create App → choose **Business**.
2. Add the **Instagram** product (sometimes listed as Instagram Graph API).
3. In **Settings → Basic**, copy the **App ID** and **App Secret**.
4. Open **Graph API Explorer** (Tools → Graph API Explorer).
5. Pick your app in the top right, then **Generate Access Token**, and tick those four permissions.
6. Copy the token it gives you.
7. In Kestrel: **Publishing → Advanced**, paste the App ID, App Secret and token, and press **Connect
   Instagram**.

Kestrel does the long-lived token exchange and finds your linked Instagram account itself. If it cannot
find one, the usual cause is step one: the account is still a personal profile, or no Facebook Page is
linked.

## Let an AI assistant walk you through it

Meta renames these screens often, so a written guide ages badly. If you get stuck, paste the prompt
below into ChatGPT, Claude or whatever you use, and it will walk you through the current version of the
interface and help with whatever error you hit.

The **Copy setup prompt** button in Kestrel (Publishing → Advanced) puts exactly this on your clipboard:

```
I'm setting up Instagram Reels publishing through Meta's Graph API, for a desktop app I run myself.

I need to end up with three things:
1. A Meta App ID
2. A Meta App Secret
3. A short-lived USER access token with these permissions:
   instagram_basic, instagram_content_publish, pages_show_list, pages_read_engagement

My app exchanges the short-lived token for a long-lived Page token itself, so I only need the
short-lived one.

My setup: an Instagram Professional account (Creator or Business) linked to a Facebook Page.

Please walk me through it one step at a time, on the CURRENT Meta developer interface, and wait for me
to confirm each step before moving on. Tell me exactly what to click and what each screen looks like.
If I report an error, help me work out which of the prerequisites is missing.

Do not ask me to paste the App Secret or the token to you — I only need to know where to find them.
```

That last line matters. **Never paste your App Secret or access token into a chat with anyone**, including
an AI assistant. They are the keys to posting as you. Kestrel stores them on your own PC and sends them
only to Meta.

## When it is working

Tick **Instagram** under "Where to post". Instagram Reels then go straight from your PC, and Upload-Post
is only used for whatever other platforms you have ticked. The Publishing tab's status line tells you
which route each platform is taking.

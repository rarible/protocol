---
title: Instagram to NFT service with Rarible Part 1
description: How to use the Rarible Multichain Protocol to find the NFT you need?
---

In this tutorial, you're going to learn how you can build a CocoNFT clone. What is CocoNFT, you’d probably ask? It’s a service that allows you to mint your Instagram posts as NFTs. I’ve broken down this article into a few sections.

**1. How to connect your Instagram account to the application,**

**2. How to connect your Metamask wallet to the application,**

**3. How to create an NFT out of a post from your IG account, which can then be sold.**

Project is splitted into a 2 part series. Including everything into one article would feel overwhelming.

**In the first part** (the one you’re currently reading), we're going to explain how to let users Authorize their Instagram accounts on the app, so they can fetch their photos.

**In the second part**, we’re going to dive deeper into integrating the application with Metamask and many different wallets. This will allow users to interact with a bunch of different blockchains, such as Polygon, Ethereum, Flow, Tezos, to name a few. All of this will be done using Rarible Protocol APIs/SDK.

**Table of content:**

**1. Create an Instagram app that can authorize a user**

**2. Get all necessary tokens that are needed to get user media**

**3. Fetch media details**

And that’s the plan for today 👆.

Let’s get started 🔥.

Psst… If you want to follow along with the finished code, here is the GitHub repo: [https://github.com/kolberszymon/nftig](https://github.com/kolberszymon/nftig)

### 1. Create an Instagram App that can authorize a user

Since scraping websites like Facebook or Instagram is a daunting task, it’s much easier to just use their API, because, well… they provide it. First, you have to go to the [Facebook for Developers website](https://developers.facebook.com/). There, you have to go to “My Apps”.

![Right Top Corner of the Website](./img/0*pi5IHLFP5xCDGGu-.png)

Click the big green button “Create an app” (no screenshot included here, because you won’t miss it for sure).

![Choosing an App Type](./img/0*DT9fMPJ-216cQDyF.png)

After that, you can choose an app type. There are quite a few different types here, but let’s select “Consumer”.

![Apps Dashboard](./img/0*Ka6t8i4BwPTCJqTH.png)

From here, we can set up more products. Since we’re focused on Instagram, click the “Set Up” button under the “Instagram Basic Display” option.

![Instagram Basic Display error](./img/0*RaDKcU0jjUsRtXk8.png)

From now on, you should see Instagram’s Basic Display on the left sidebar. If you’re following this tutorial, you should also see a big red error. Don’t worry, we’re going to solve it now.

Go to Settings > Basic. You can then see App ID and App Secret. While we’re on top of the page, you should also add the Privacy Policy URL and User Data Deletion. These fields are mandatory. What’s funny is that it can be a totally fake URL (that would kinda breach the ToS of Meta and GDPR, I think). It just needs to have HTTPS and return status 200. I’m using [\*\*https://httpstat.us/200](https://httpstat.us/200) \*\*which is basically a tool that always returns the 200 status code.

![Settings / Basic Page with Privacy Policy and User Data Deletion URL inserted](./img/0*yQK1YpB6bMuzPduE.png)

There is one more thing that we have to do while we are still on the Settings / Basic page: adding a platform. Localize a big “ Add Platform” button on the bottom, click on it, and you should see the following popup. Select the website option.

![Popup, which appears after clicking the “Add platform” button on the bottom of the page](./img/0*nxoKhE33vvl4g5MU.png)

Add a website URL.

![Okay, that’s all the configurations in Settings/Basic.](./img/0*1MRnFi3gqNtfQoM3.png)

After we filled in all required URLs and added a platform, we are able to create a New App on Instagram Basic Display.

![Previously unavailable button on Instagram Basic Display](./img/0*o8JevD2CR90BgrM4.png)

You’ll need to provide the correct URLs. This step is very important, becouse the Valid OAuth Redirect URI is an address where the Instagram Authorize window will redirect you with the Authorization Token as a query parameter. So in an ideal scenario, you would pass your backend API address here, save the token in the database, and then redirect the user to the proper page.

![Needed URIs](./img/0*rI_B_dbH5hiGSWxL.png)

The next step is to add the following options to submission. They are required to allow us to fetch user data.

![Submissions which you have to add in order to be able to fetch user medias](./img/0*duc9j4DB5YXxrQTg.png)

Okay, the setup step is already done…almost 🥰.

You also have to add an Instagram test user to be able to use the Instagram API in development mode. You can do it by going to Roles / Roles on the sidebar, and adding Instagram testers.

![](./img/0*KQDJIsXhJc3db9jh.png)

Finally… the last step. You have to agree on becoming a test user. You can do it by going to Instagram > Settings > Apps and Websites.

![Accepting the invitation](./img/0*2M5phDPq880evxZs.png)

That’s the end of the 1st section. You’ve learned:

**— How to create a Facebook App**

**— How to create an Instagram App**

**— How to invite a Test User**

### 2. Get all necessary tokens needed to get user medias

When it comes to the tokens, we’ll need:

**1. Authorization Token** — The one we receive after informing we want to authorize our app. The Authorization Token is one-time usage only, but if you mess this step up don’t worry, you can always show it again.

![Authorize App screen](./img/0*QwLn23eF25f73ETD.png)

**2. Short-Lived Token** — At this stage, we have an Authorization Token, which we can trade for the Short-Lived Token. It allows us to query the Instagram API for 60 minutes! That’s where its name came from. But we can also go one step further, and trade it for…

**3. Long-Lived Token** — After obtaining it, you’re able to use it for up to 60 days. You’re also able to extend it after 24 hours from creating it. What it means in practice, is that you will not have to ask a user for an Authorization again. Big UX win! 👊

Before we learn how we can obtain it, you should prepare the two values below. They will interchange in a lot of requests.

- **APP_ID**

- **APP_SECRET**

We can get both of them on the FB For Developers Instagram Panel.

**1. Authorization-Token**

In order to retrieve the Authorization Token, first, we have to prepare the following URL:

```
https://api.instagram.com/oauth/authorize?client_id=6201234567890178&redirect_uri=https://httpstat.us/200&scope=user_profile,user_media&response_type=code
```

You’ll need a few parameters here. Client_id, redirect_uri, the scope of granted access. We talked about all of them earlier. After the URL creation, simply paste it to the browser. Then, the authorize page will pop up like it was shown earlier. Click on Authorization, and it will take you to the Redirect URI, which you’ve provided, **BUT **(and that’s the fun part) with an added code parameter. An example of a URL looks like this:

```
https://httpstat.us/200?code=AQBvJwCZtYdj1zLH_5myoAA1GRRpDhs1vcHFMzB4gvRk6dLkq5dNd24EVZ5FD9WoqQhfSuo6arUB17MPu2gRqEzP6EpsAl-9_2eC9-L6mWYQdWDyarkwDSNEs8T3gvoH-WLMHzhwwd6DJqP5PxJGf2ve53m7aGMEua3MzV8FZQVz5AfwWPN3G87n25jMBGgGGVj6G4pxJ9HqzNKmdpYK8GHKnRn_G03scHtUraFlEX5faCvz6ZO7Xw#_
```

This is the code we require, so copy it and delete the last two characters, “#\_” to be precise. They are always added, and you have to delete them.

**2. Short-Lived Token**

In order to obtain this one, we’ll need to do a POST request with form data added. We’ll need:

- **CLIENT_ID**: which you can grab on FB For Developers / Instagram Display Page, it’s called App ID on the page

- **CLIENT_SECRET**: same as above, only it’s located to the right

- **GRANT_TYPE**: “authorization_code”

- **REDIRECT_URI**: redirection URI which you’ve provided

- **CODE**: Authorization Token which we obtained in the previous step

If you’re using Postman, which I highly recommend for doing HTTP requests, your page should look similar to mine. Names in between curly braces are called Environment Variables. You can set them in global, and reuse them throughout the app.

```
https://api.instagram.com/oauth/access_token
```

![Needed form parameters presented in Postman](./img/0*295rmhVGZ0GiCRTE.png)

After sending a successful request, you should see the following answer.

![Example response object](./img/0*vbv1z8Q2d-Hx5a0D.png)

If you mess something up, just read the error description and repeat the step to obtain the Authorization Token. Remember that it can only be used once. Going back to response values, **access_token **is our short-lived token, and user_id is, well, our user ID. It doesn’t change at all, so you can also store it in the Global Vars on Postman. Congratulations! You’re now able to fetch user data! For now, it’s valid only for 60 minutes, so let’s work on that right now.

**3. Long-Lived Token**

In order to change the Short-Lived Token into the Long-Lived one, you’re going to have to do a GET request to this address:

```
https://graph.instagram.com/v13.0/access_token?client_secret={{APP_SECRET}}&access_token={{ACCESS_TOKEN}}&grant_type=ig_exchange_token
```

![View in Postman](./img/0*HyKrhOKzKnwrH9LD.png)

In exchange, you’ll get a self-explanatory response. Grab an access_token value, and you’re good to go. You have a Long-Lived Token, now!

![Response with long-lived token example](./img/0*-i1ftezk76BgHbsf.png)

### 3. Fetch media details

We’ve come a long way, but we’re finally here! After creating an Instagram App and getting a Long-Lived Token, we’re now ready to do some coding. Since we don’t really have an HTTPS on localhost, we’ll just use an access_token straight from the code. If you’d like to go live with that, you just need to change a few things. Maybe create some sort of backend API, replace the Instagram Redirect URI to your website’s one, and take it from there. This is just for tutorial purposes, so I won’t do that here. Of course, there are a lot of different ways to achieve the same goal, so it’s better to focus on concepts here.

The workflow is as follows:

**1. Fetch IDs of user media**

**2. Fetch media URL, using previously obtained IDs**

The URLs which you’ll need in order to get those data are:

**3. Fetch IDs of user media**

```
https://graph.instagram.com/v13.0/{{USER_ID}}/media?access_token={{LONG_LIVE_TOKEN}}&fields=id,timestamp
```

![](./img/0*Y95FhknsY57YJoBL.png)

Exemplary response

Ids are the MEDIA_ID.

**4. Fetch media URL, using previously obtained IDs**

```
https://graph.instagram.com/v13.0/{{MEDIA_ID}}/media?access_token={{LONG_LIVE_TOKEN}}&fields=media_url,media_type
```

Where MEDIA_ID are the IDs fetched earlier.

Finally, — here comes my favourite part:

\*\*To the code soldiers! 🥳

Compared to the work that we’ve already done, it will be pretty quick.

**1. Fetch IDs of users’ media**

![Fetching media IDs](./img/0*F2l2pgMePlOzoSsE.png)

**2. Fetch portion of retrieved posts**

Since there is an API requests rate limit, which equals 200 requests per hour per token, I prefer to fetch posts in portions when a user actually wants to fetch more than X. Thanks to that, we’re saving our requests rate, as well as internet throughput.

![Fetching portion of posts](./img/0*ZF_OQZ0uZ4NH-Bfw.png)

**3. Display fetched media**

![Mapping over created MediaDetail array](./img/0*bRQ05XUoDyKgG241.png)

In the final step, you just have to map the media details array and use media_url as an image source.

### Summing it up

We know that the article was quite big, but look how much you've done. You’ve created an Instagram App, set it up, authorized a user, created a long-lived token, fetched IDs of users’ media, got media URLs, and in the final step, displayed it.

Feel free to read it again, especially the token creation part, just to understand better how the flow works.

In the second part, you'll implement the NFT creation out of Instagram posts.

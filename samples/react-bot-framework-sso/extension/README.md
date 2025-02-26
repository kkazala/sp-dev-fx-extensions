# Microsoft Bot Framework Web Chat with SSO

## Summary
An extension sample that uses the [botframework-webchat module](https://www.npmjs.com/package/botframework-webchat) to create a React component to render the Bot Framework v4 webchat component. This extension is a single sign-on demo for on behalf of authentication using OAuth.

> When dealing with personal data, please respect user privacy. Follow platform guidelines and post your privacy statement online.

## Used SharePoint Framework Version

![1.10.0](https://img.shields.io/badge/drop-1.10.0-green.svg)

## Applies to

* [SharePoint Framework Extensions](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/extensions/overview-extensions)
* [Office 365 developer tenant](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant)
* [Microsoft Bot Framework](http://dev.botframework.com)

## Prerequisites

> You need to get familiar with [the extension web chat sample](Placeholder) first as this sample is based on that extension sample.

> You need to have this [bot](../bot/) created and registered using the Microsoft Bot Framework and registered to use the Direct Line Channel, which will give you the token generation endpoint needed when adding this extension to the page. For more information on creating a bot and registering the channel you can see the official web site at [dev.botframework.com](http://dev.botframework.com).

## Disclaimer
**THIS CODE IS PROVIDED *AS IS* WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**

---

## Minimal Path to Awesome

- Clone this repository

- Edit "BotFrameworkChatPopupApplicationChat.tsx" file to set your bot endpoint (`props.botEndpoint`) directly like `https://YOUR_BOT.azurewebsites.net` for testing purpose (instead of setting it in the Tenant Wide Extensions list):

    ```ts
    generateToken(props.botEndpoint, md5(userId)).then((token: string) => { //change props.botEndpoint to the endpoint directly if you want to test it
    if (token) {
        setDirectLine(createDirectLine({ token }));
    }
    });
    ```

- Edit "BotSignInToast.tsx" file to set your AAD scope uri(`scopeUri`) with `api://YOUR_APP_ID` directly like `api://123a45b6-789c-01de-f23g-h4ij5k67a8bc` for testing purpose:

    ```ts
    return tokenProvider.getToken(scopeUri, true).then((token: string) => {
    ```

- Add the following config to ./config/package-solution.json:
    ```diff
        "webApiPermissionRequests": [
    +     {
    +       "resource": "<YOUR_APP_ID>",
    +       "scope": "<YOUR_AAD_SCOPE_NAME>"
    +     }
        ],
    ```

- Refer [Connect to Azure AD-secured APIs](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/use-aadhttpclient) to publish and approve permissions from admin site

- In the command line run
    ```bash
    cd ../extension
    npm install
    gulp serve --nobrowser
    ```

- Open up a SharePoint modern page and add the following string to your URL:

    ```
    ?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"f50b07b5-76a5-4e80-9cab-b4ee9a591bf6":{"location":"ClientSideExtension.ApplicationCustomizer"}}
    ```

## Deploy

If you want to deploy it follow the steps [here](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/extensions/get-started/hosting-extension-from-office365-cdn) and add the following properties to the "Component Properties" column in the Tenant Wide Extensions List:

```json
{
    "allowedSites":["https://YOUR_TENANT.sharepoint.com/sites/abc"],
    "botEndpoint":"https://YOUR_BOT.azurewebsites.net",
    "botScopeUri":"api://YOUR_APP_ID"
}
```

## Features

This Extension illustrates the following concepts on top of the SharePoint Framework:

- Using the Bot Framework webchat React component as some kind of flyout element in modern pages
- Adding a bot to modern pages and let users interact with a bot hosted in the Azure Bot Service
- Demo single sign-on for on behalf of authentication using OAuth

<img src="https://pnptelemetry.azurewebsites.net/sp-dev-fx-extensions/samples/react-bot-framework-sso/extension" />

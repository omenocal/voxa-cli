# voxa-cli

The perfect toolkit for your Voxa app.

[![Build Status](https://travis-ci.org/VoxaAI/voxa-cli.svg?branch=staging)](https://travis-ci.org/VoxaAI/voxa-cli)
[![Code Coverage](https://codecov.io/gh/voxaai/voxa-cli/branch/staging/graph/badge.svg)](https://codecov.io/gh/VoxaAI/voxa-cli)

## Install it in your Voxa app

```
$ yarn add voxa-cli
```

## Roadmap

| Feature                  | Description                                                     | Completed | Version |
| ------------------------ | --------------------------------------------------------------- | :-------: | :-----: |
| **Multicommand support** | Organize project to support multiple commands                   |    ✅     |  2.0.0  |
| **Command Init**         | Allow user to create an empty (default) interaction json Voxa 3 |    ✅     |  2.0.0  |
| **Command Interaction**  | Improvements to interaction command                             |    ✅     |  2.0.0  |
| **Typescript**           | Move to project to Typescript                                   |    ✅     |  2.0.0  |
| **README.md**            | Update/Improve repo README.md                                   |    ❌     |  2.0.0  |

## Getting started

With the Voxa-cli you can scaffold a full Voxa project ready to get started to code your voice app for Amazon Alexa, Google Assistant, Telegram and Facebook Messenger.

You can also create interaction model and publishing information for your Alexa skills. Voxa-cli supports many sources like google spreadsheet, office 365, local .xlsx, .ods, .fods files to manage your interaction model information and publishing information.

### How to generate a Voxa project

As simple as:

```
$ npx voxa create
```

You'll be prompt to answer several question like:

- The name of your project
- The language of preference for your Voxa app (Javascript or Typescript)
- The platform for your Voxa app
- Usage of the canfulfill intent if you'll create an Alexa skill
- Analytics you can use (using Voxa plugins)

Once done you'll be ready to start working on your next voice app.

### How to connect with Google Spreadsheet

To programmatically access your spreadsheet, you’ll need to create a service account and OAuth2 credentials from the Google API Console. If you’ve been burned by OAuth2 before, don’t worry; service accounts are way easier to use.

Follow along with the steps and GIF below. You’ll be in and out of the console in 60 seconds.

Go to the Google APIs Console.
Create a new project.
Click Enable API. Search for and enable the Google Drive API and Google Sheet API.
Create credentials for a Web Server to access Application Data.
Name the service account and grant it a Project Role of Editor.
Download the JSON file.
Copy the JSON file to your code directory and rename it to client_secret.json

![alt text](https://www.twilio.com/blog/wp-content/uploads/2017/03/z5P3Wgwb468knWrP27VvpiWAAfZGuOu3gbxUrmi4RYQ2UmZr3wbDM1qTDEasNgsZYAhkDRQryo2vJ3LpvYekSbqntIG_YhO1RiIpVFmGrBwzDwASc8UTnGruTmnZTVZgAkGxPRgQ.png)

There is one last required step to authorize your app, and it’s easy to miss!

Find the client_email inside client_secret.json. Back in your spreadsheet, click the Share button in the top right, and paste the client email into the People field to give it edit rights. Hit Send.

![alt text](https://www.twilio.com/blog/wp-content/uploads/2017/03/2pzVvPzuNHokBSR2KXoPB9XC15xBF-qBCRJJq0Ut987IkqDVeL3sNdqY2oQj-1V1-2X-SdU33jAuwQ88_XxH703HFpoe7slpVUIniinIqbpz2zD6U2pd77C1iXT0Kzd4qFWb9pI0.png)

Finally copy the client_secret.json in the root of the project. `client_secret.json`

### How to connect with Office 365 workbooks

We will need an AAD (Azure Active Directory) and register out application. Create one by using the azure.portal. Your Azure Active Directory ID can be found in Azure Portal > AAD Properties

#### Registering an OAuth App

- Sign in to the Azure portal.
- If your account gives you access to more than one, select your account in the top right corner, and set your portal session to the desired Azure AD tenant.
- In the left-hand navigation pane, select the Azure Active Directory service.
- Select App registrations and then select New application registration.
- When the Create page appears, enter your application's registration information:
  - Name: Enter a meaningful application name
  - Application type:
    - Select Web app/API for client applications and resource/API applications that are installed on a secure server.
  - Sign-On URL: For this application enter any sign on URL
- From the Main Panel grab the application ID (client_id)

> More info https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-v1-add-azure-ad-app

- Create a new Client Secret: Navigate to App > Keys > Passwords and add a new key.
  - Name (description): enter a descriptive name for the key so you later know that the client application is using it.
  - Expires: Choose "Never Expire," unless you want to change your key every year or two.
  - Click Save - a new Client Secret will be generated for you. This will be the only time you will see the Client Secret, so you better copy it to a secured location otherwise you won't be able to retrieve it again!

#### Configuring App Permission

Now that we have created an app, we have to configure its permissions.

- Setup app permission: Navigate to App > Required Permission > Add > Select an API > "Microsoft Graph" > Select Permission. We see a list of Graph related permissions. Here we can select the permission our app should have.
- Select the following permissions `Read files in all site collections`, `Read directory data`
- Click the button `Grant Permissions`.
- Each time we change permissions we need to give `Admin consent`. With an Admin user go to

```
https://login.microsoftonline.com/{TenantDirectory}.onmicrosoft.com/adminconsent?client_id={ApplicationID}
```

Finally create a file and name it `azure.secret.json` in the root folder of your project with the following values.

```json
{
  "client_id": "XXXXXX",
  "client_secret": "YYYYYYY",
  "tenant_directory": "ZZZZZZZZ" // could be tenant directory name or id
}
```

### Interaction.json

Once you have the OAuth2 you should create the interaction.json.
Create a new file on your skill root project `./interaction.json` and paste the following snippet. Replace all the values you need.

```json
{
  "platform": ["alexa", "dialogFlow"],
  "spreadsheets": [
    "GOOGLE_SPREADSHEET_URL",
    "OFFICE365_WORKBOOK_URL",
    "LOCAL_EXCEL_FILE",
    "LOCAL_EXCEL_FOLDER"
  ]
}
```

Finally execute it and voilà :flushed:

```
$ npx voxa interaction
```

### Options

- **spreadsheets**: Array of spreadsheets. Each sheet should be a interaction model for a specific locale. Spreadsheet can also be about publishing information. Make sure to review [Interaction spreadsheet structure]({{ site.url }}/docs/interaction-spreadsheet) and [Publishing spreadsheet structure]({{ site.url }}/docs/publishing-spreadsheet)
- **platform**: We currently support Alexa and Dialog Flow interaction models. Make sure to review [platform structure]({{ site.url }}/docs/platform)

### Other links

- [Interaction spreadsheet structure](/docs/interaction-spreadsheet)
- [Publishing spreadsheet structure](/docs/publishing-spreadsheet)
- [Content structure](/docs/interaction-spreadsheet#tabs-to-download-should-have-the-following-structure)
- [Local manifest](/docs/local-manifest)
- [Platform](/docs/platform)

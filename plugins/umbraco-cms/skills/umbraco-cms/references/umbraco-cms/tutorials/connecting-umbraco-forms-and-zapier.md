# Connecting Umbraco Forms and Zapier | CMS

This guide takes you through the steps of connecting your Umbraco Forms to Zapier.

is an “if this, then that” tool that allows you to automate workflows between the different web apps you use. Zapier has integrations to more than 2,000 web apps and lets you connect to your accounts with a few clicks without any code.

Umbraco Forms stores entries in the backoffice. It has a set of default workflow types that you can use when a new form entry is submitted. To use this data in other applications, such as your Customer Relationship Management (CRM) or marketing automation platform, you need integrations to those platforms. Integration with Zapier can be done using the default workflows in Umbraco Forms. All without having to write any additional code.

This enables marketers and editors to make automated workflows that pass data between the web apps they use without having to involve a developer.

This tutorial is for all users of Umbraco and does not require any particular skills to be performed. It is especially useful for marketers who get the freedom to make integrations and automate tasks in a simpler and faster way.

Here is what you will need for this tutorial:

A paid Zapier account (Premium apps are unavailable in the free plan)

Umbraco Forms

A Google account (only necessary if you want to follow the last example in the guide)


The first step is to generate the webhook URL that your Umbraco Forms has to send data to. This is done by logging into your Zapier account and clicking “Make a Zap”

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4371684e7a1c273afdf64a72c169ee5aacffbadf%252FzapierMakeZap.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1944d58a&sv=2)

The next thing to do is pick an app in the “When this happens…” box. This is your trigger and determines when your Zap will start. Select the “Webhooks by Zapier” app

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b726451f36a1e23442052cea08ccb61b9cb0c081%252FzapierFindWebhooksTrigger.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e2c70aa2&sv=2)

Now select the “Catch Hook” trigger event and click continue.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e60d22e1a52f10061d16c23800f62a46fa2d4510%252FzapierWebhooksCatchHook.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=17a26c36&sv=2)

Now you will get a “Custom Webhook URL” that you will need for your Umbraco Forms.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f80b3b55f992dd484bfb295fb9c1986c1bfc711b%252FzapierCustomWebhookURL.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=811aa26&sv=2)

Copy this URL and have it ready for later. You will need it when you set up your Umbraco Forms workflow. Now we have to go into the Umbraco backoffice, but keep the Zap you created open. We will get back to it later to finish setup.

Now it’s time to login to the Umbraco backoffice so you can create your form. If you already have a form you want to connect you can skip to the next step.

To create a form you can follow this tutorial with step-by-step instructions: .

Once you have created your form you are ready to set up the workflow.

Once you have set up your form, it is time to add the “Send form to URL” workflow to your form. This will allow you to post your data to the Zapier webhook URL you generated earlier.

Go to your form in the backoffice and click on “configure workflow”. In the “On Submit” workflow you click “Add workflow”.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-82eaa8e0022544a51b1dbc2157e37a5e38c74626%252FumbracoFormsAddWorkflow.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=abc91a2d&sv=2)

Now choose the workflow “Send form to URL”.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b9d22c3dd3d47ff38e24d0eead4a029a444778a2%252FumbracoFormsSendFormToURLWorkflow.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7707fce8&sv=2)

After giving the workflow a descriptive name, you paste in the webhook URL from Zapier in the “Url” field and choose POST in “Method”. Leave “Fields”, “User” and “Password” blank.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c64fd92c7ebe45abdc19185024a71869056828cd%252FumbracoFormsSendFormToURLWebhook.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a0ae1a69&sv=2)

Now your workflow is ready. Submit your changes and save your form.

Now your form is ready to send data to Zapier and any entry submitted will be posted to the Zapier webhook URL.

To set up field mapping and actions in Zapier your form needs an entry. If this is a new form, add it to a page and submit an entry ().

Here is the form and the fields that were submitted for this tutorial.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a7f91d88d4bb32204e4dc82d7de676f85bef3f67%252FumbracoFormsFieldsSubmitted.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bdb80d01&sv=2)

Once you have an entry in your form you are done in the Umbraco backoffice. Now it is time to go back to Zapier and finish setting up your automation.

In Zapier, open up the Zap you started setting up in the first step of this guide. In that Zap we are now ready to continue the setup of our webhook trigger. Start by clicking continue and get to the “Find Data” step.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4f42cf91301ce17804f8f0136eb4ba34fba9c744%252FzapierFindWebhookData.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=aa39960a&sv=2)

Now click on “Test trigger”. If there is an entry to the form it should look like this.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1b7ce88686a949997954e73fe7fabd542a36510d%252FzapierWebhookDataFound.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9a6df67a&sv=2)

Now you have data to further map in your Zap and can continue choosing the action for the Zap. If Zapier does not find any data, try to submit a new form entry.

After clicking “continue” you are now starting on the “Do this…” action of your Zap.

Up until now, the steps will be the same for everyone. Now that you have connected Umbraco Forms and Zapier it is up to you to decide where you want to send the data.

In this tutorial you will get an example of how you can send your data to Google Sheets. This allows you to see how a finalized Zap looks like.

As a “Do this…” action you want to send data to Google Sheets. Before doing so in your Zap you need to ensure that you have created a Google Sheet to receive the data. You also need to connect your Zapier account to your Google Sheets account.

Once you have done these steps it is time to finish the setup of the Zap.

First thing to do is find the “Google Sheets” app in the “Do this…” action.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c6f0afae41f8a7dbda230722a39a13a3cc1be45a%252FzapierGoogleSheetsApp.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=834d0c9c&sv=2)

Now choose the Action event “Create a spreadsheet row” and continue.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-55488c86bbc722bda2211b02e5a31c4bb4249294%252FzapierGoogleSheetsActionEvent.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=aa6c6bc1&sv=2)

Now you need to choose the Google Sheets account you want to connect to. If you have not set this up yet, you will be prompted to do so. Once connected you choose that account and click continue.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0d5c7502a5314a0c4334eaf96aa980dedca560f6%252FzapierGoogleSheetsAccount.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c678055a&sv=2)

Now you can choose which Google Drive to use, find the spreadsheet and choose the worksheet that you want to send the data to. After doing so, you will get a list of possible fields that you can post your data to.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-cf7b117642437ddf745d6b4c9f12a8075f6cc846%252FzapierGoogleSheetsPossibleFields.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1aae8d94&sv=2)

The fields showing are all columns in your spreadsheet that have a name in row 1. To map the input data to the different fields in the spreadsheet follow these steps:

Select the “Type or insert…” field.

Choose which data to put in the field.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-205d25a25143440143582e9e1f0947b8b1c44bcf%252FzapierGoogleSheetsWebhookData.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e17e7fbe&sv=2)

The data that was caught by the webhook will all be dynamic and you will want to pick the fields here. That way, when a new entry comes in, the field will dynamically insert the data they submitted for that field.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-55206da952a6dc588ad020d17fe22e37a5e16cc8%252FzapierGoogleSheetsDataMapped.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f3929d11&sv=2)

Once you have mapped all of the fields it is time to click “continue” and test if the data is sent correctly to our spreadsheet.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-93a4d3d5db4ada08674bb16c067675aed306c293%252FzapierGoogleSheetsTest.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ec84be1c&sv=2)

Click “Test & Continue” and wait for it to process. Once it is done, go to the spreadsheet you created and see if the data is there.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ae50587e871f13e4b5daf746dc19bcb6bcc30eb3%252FgoogleSheetsData.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3e1c2313&sv=2)

Tada! Now your Zap is ready and can be activated to automatically add form entries to Google Sheets. To activate the Zap you go back to your Zap and change the toggle from “Off” to “On”. Now it will be waiting for new form entries and be ready to send them to Google Sheets.

If you want to connect multiple forms to Zapier you can follow the above steps to do so. Remember to add individual Zaps to each form if the data being sent is different or you want to use different actions for the data.

You can reuse the same Zap and webhook URL if all data sent to Zapier is formatted in the same way. Otherwise errors will occur.

That’s it. Now you are ready to connect Umbraco Forms to Zapier and can use it to send data to the tools you choose.

Last updated

Was this helpful?
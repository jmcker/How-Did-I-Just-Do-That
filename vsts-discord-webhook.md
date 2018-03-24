
## VSTS Build Status Notification for Discord Channel

Use a Discord WebHook to send VSTS build status notifications to a Discord channel.


### Create a Discord WebHook
This is based on the instructions from the Discord support article below.
For a more detailed explanation, including images, see the first source link.

1. Go to *Server Settings* in the menu under the desired server's name.
2. Under *WebHooks*, create a new WebHook.
3. Give it a name, select the desired channel to post to, and **copy the WebHook URL**.

### Integrate the WebHook with VSTS
1. Open the project home for which you want to add the WebHook.
2. Navigate to the *Setting (gear icon)->Service Hooks* page.
3. Create a new subscription by selecting the + button near the top left.
4. Select *Slack* as the service and hit Next.
5. Configure the trigger to your liking and hit Next. The default settings will send notifications for every build status on every build configuration in the project.
6. Paste the Discord WebHook URL from above into the *Slack WebHook URL* box. **Add `/slack` to the end of the Discord URL.** Adding `/slack` turns the URL into a Discord Slack-Compatible WebHook.
7. Select *Test* to ensure that everything worked and *Finish* to save the service.


Source:
- https://support.discordapp.com/hc/en-us/articles/228383668-Intro-to-Webhooks
- https://discordapp.com/developers/docs/resources/webhook#execute-slackcompatible-webhook
- https://docs.microsoft.com/en-us/vsts/service-hooks/overview?view=vsts
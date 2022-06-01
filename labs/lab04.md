# 4 - GitHub Apps
In this lab you will develop a GitHub App using the Probot framework.
> Duration: 15-20 minutes

References:
- [GitHub Apps](https://docs.github.com/en/developers/apps)
- [Creating a GitHub App](https://docs.github.com/en/developers/apps/building-github-apps/creating-a-github-app)
- [GitHub Apps - Probot](https://probot.github.io/docs/)
- [GitHub Apps - Probot - Best practices](https://probot.github.io/docs/best-practices/)
- [GitHub Developer - GitHub Apps Cheat Sheet](https://github.com/github-developer/github-apps-cheat-sheet)
- [Creating a GitHub app with create-probot-app: Creating my first GitHub app with Probot - Part 1 (andrewlock.net)](https://andrewlock.net/creating-my-first-github-app-with-probot-part-1-create-probot-app/)

## 4.1 Developing a GitHub App

1. Follow the guide [Probot - Developing an app](https://probot.github.io/docs/development/) to develop your first GitHub App.
2. Choose the `basic-js` template and follow the steps to generate, run, configure, and install your GitHub App.
3. Once installed on your repository, use `npm start` to start your application and listen to webhook events.
4. Test your application by creating a new issue on the installed repository
5. Update the `index.js` file to add the following listener:
```javascript
  app.onAny(async (context) => {
    app.log.info({ event: context.name, action: context.payload.action });
  });
```
6. Run the application `npm start`
7. Navigate to your repository where the application is installed
8. Add a new label to an existing issue, push new code or update the repository settings
9. Watch the application logs for triggered events
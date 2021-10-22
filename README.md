# Schedule Build Hook Trigger

Use this action to schedule triggering build hooks on services like Netlify and Vercel.

If you run a blog or publish other time sensitive content on your static site, you might schedule content for the future. This means you need to trigger builds at daily intervals (or more often) to check if any new content needs to go live. This action does that, by calling your build hook on a schedule.

## Create a build hook

Before you can use this action, you need create a build hook for your site. On [Netlify](https://docs.netlify.com/configure-builds/build-hooks/) `Site settings` > `Build & deploy` > `Build hooks`. On [Vercel](https://vercel.com/docs/concepts/git/deploy-hooks) in `Settings` > `Git` > `Deploy Hooks`.

## Add it to secrets

For security, you need to keep your build hook secret, so don't add it directly to your action (which will be stored in your repository). [Vercel](https://vercel.com/docs/concepts/git/deploy-hooks) state this in their documentation:

> When you create a Deploy Hook, a unique identifier is generated in the URL. This allows anyone with the URL to deploy your project, so treat it with the same security as you would any other token or password.

So, add your build hook in Github Secrets `Settings` > `Secrets` > `New repository secret`. The **Name** should be `BUILD_HOOK` and the **Value** will be the build hook url from Netlify or Vercel.

## Use the action

You are all set up now to use the action! By default, the action runs at 9am Weekdays (Monday - Friday). Replace `"0 9 * * 1-5"` if you need to make changes.

```
    # Runs at 9am every weekday
    - cron: "0 9 * * 1-5"
```

You can tweak this to suit your schedule requirements, here's an awesome [free cron schedule editor](https://crontab.guru/#0_9_*_*_1-5) to create your own schedule.

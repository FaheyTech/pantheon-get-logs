# pantheon-get-logs
This utility pulls all nginx logs for a given Pantheon site, generate an HTML report, and upload that report to a Pantheon site to be able to view it in a browser.

![Screenshot of html report](static/Server-Statistics.png)

- Triggered via workflow_dispatch.
- Uses GoAccess to generate an HTML report.

## Setup
- Fork this repo, so that you can customize it for your own personal needs.
- Add a `PANTHEON_MACHINE_TOKEN` and `SSH_KEY` Action secrets for the repo. 
  ![Screenshot of repo secret settings action](static/repo-secret-settings.png)
  - The `PANTHEON_MACHINE_TOKEN` should be a machine token with access to the site to analyze and upload results to. 
  - Likewise, the `SSH_KEY` should be a private key associated with the account that generated the machine token, with the public key added to the Pantheon account. E.g. if you ran `ssh-keygen`, and kept the default name of `id_rsa`, you'd want to copy the `id_rsa`, and paste it in as the `SSH_KEY` secret. Then, go to the Pantheon account settings, and add the SSH key of the `id_rsa.pub`.

- User needs to configure a Slack `SLACK_WEBHOOK_URL` secret to have notification sent with a link to view the file. You could also tweak the code to use Github Actions workflow artifacts and store the HTML there, or otherwise upload it to a different host / provider.

## Usage
- Head to the "Actions" tab on your fork.
- Select the Action on the left hand side.
- Hit "Run workflow" on the right hand side.
- You can provide the inputs, and it will run. Check the progress in the Actions tab.

![Screenshot of running action](static/Actions_%C2%B7_FaheyTech_pantheon-get-logs.png)

Keep in mind - You can also trigger these programmatically with the Github API! The possibilities are endless! You essentially send a JSON payload with your inputs, e.g.
```
{
    "ref": "master",
    "inputs": {
        "site_name": "whatever-site",
        "site_environment": "live",
        ...etc
```

For more, check out [the Github Workflow API docs.](https://docs.github.com/en/rest/actions/workflows#create-a-workflow-dispatch-event)



# pantheon-get-logs
This utility pulls all nginx logs for a given Pantheon site, generate an HTML report, and upload that report to a Pantheon site to be able to view it in a browser.

- Triggered via workflow_dispatch.
- Uses GoAccess to generate an HTML report.

## Setup
- Fork this repo, so that you can customize it for your own personal needs.
- Add a `PANTHEON_MACHINE_TOKEN` and `SSH_KEY` Action secrets. 
  - The `PANTHEON_MACHINE_TOKEN` should be a machine token with access to the site to analyze and upload results to. 
  - Likewise, the `SSH_KEY` should be a private key associated with the account that generated the machine token, with the public key added to the Pantheon account. E.g. if you ran `ssh-keygen`, and kept the default name of `id_rsa`, you'd want to copy the `id_rsa`, and paste it in as the `SSH_KEY` secret. Then, go to the Pantheon account settings, and add the SSH key of the `id_rsa.pub`.
- User needs to configure a Slack `SLACK_WEBHOOK_URL` secret to have notification sent with a link to view the file. You could also tweak the code to use Github Actions workflow artifacts and store the HTML there, or otherwise upload it to a different host / provider.

## Usage
- Head to the "Actions" tab on your fork.
- Select the Action on the left hand side.
- You can provide the inputs, and it will run. Check the progress in the Actions tab.

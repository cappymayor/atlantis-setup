# atlantis-setup
This guide provides a easy way to setup atlatis locally to enable more collaborative way to deploy infra on the cloud in a work environment.

## Prerequitite
The below are prerequite for using atlantis, they must have been installed.
- Terraform - Installation guide can be found [HERE](https://developer.hashicorp.com/terraform/install) 
- ngrok - Installation guide can be found [HERE](https://ngrok.com/downloads/mac-os)
- Ensure a dedicated user with both the access and secret key has been created for atlantis to have access to all resources in AWS.

## Step 1
- Start ngrok by running the below command if you install `ngrok` via brew, copy and keep the forwarding long url, it should like this `https://3456-2003-c7-3713-91c2-3482-6209-8dd2-829c.ngrok-free.app`.
```
ngrok http 4141
```
- Start ngrok with the below command if you install `ngrok` with manual download (ensure you are in the directory of the ngrok)
```
./ngrok http 4141
```

## Step 2
- Create a random string character. You can generate one [HERE](https://www.random.org/strings/) ( Keep it also )
- Fell free to choose the length of your choice, example 18, 24 random string long.

## Step 3
- Create the repository for your project.
- This repository should be where you want to provision your cloud infrastructure from.

## Step 4
- Create a webhook from that repository
  - Go to the repository Settings
  - On the left click Webhooks
  - Click add webhook on the right
  - set Payload URL to your ngrok url with /events at the end. Ex. `https://3456-2003-c7-3713-91c2-3482-6209-8dd2-829c.ngrok-free.app/events`
  - double-check you added /events to the end of your ngrok URL.
  - set Content type to application/json.
  - set Secret to your random string you generated on `Step 2`.
  - select Let me select individual events.
  - check the boxes
    - Pull request reviews
    - Pushes
    - Issue comments
    - Pull requests
    - leave Active checked
    - click Add webhook

## Step 5
- Create github token for Atlantis to communicate with Github
  - Watch this 3 mins [Video](https://www.youtube.com/watch?v=m5SChqEi314) on how to do that
  - Please keep the token safe.
 
## Step 6
- Create a start.sh file with the below to start your atlantis application
```
#!/bin/bash
URL="Your ngrok url in Step 1"
SECRET="Your random string generated in Step 2"
TOKEN="Your Github Token in Step 5"
USERNAME="Your Github Username"
REPO_ALLOWLIST="github.com/YourGitHubUsername/YourRepositoryName"

atlantis server \
--atlantis-url="$URL" \
--gh-user="$USERNAME" \
--gh-token="$TOKEN" \
--gh-webhook-secret="$SECRET" \
--repo-allowlist="$REPO_ALLOWLIST"
```


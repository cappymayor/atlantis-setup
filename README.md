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


# atlantis-setup
This guide provides a easy way to setup `Atlantis` locally to enable more collaborative way to deploy infrastructures on the cloud in a work environment.

## Workflow Image

<img width="1377" alt="Screenshot 2025-06-06 at 14 56 06" src="https://github.com/user-attachments/assets/210d18d8-7647-41b7-bb4b-670de0378f08" />


## Prerequitite
The below are prerequite for using `Atlantis`, they must have been installed.
- Terraform - Installation guide can be found [HERE](https://developer.hashicorp.com/terraform/install) 
- ngrok - Installation guide can be found [HERE](https://ngrok.com/downloads/mac-os)
- Ensure a dedicated user with both the access and secret key has been created for atlantis to have access to all resources in AWS and saved in this file path `.aws/credentials` in your home directory. The file should look like something below.
  - ```
    [default]
    aws_access_key_id = xxxxxxx
    aws_secret_access_key = xxxxxxxx
    ```

## Step 1
- Start `ngrok` by running the below command if you install `ngrok` via brew, copy and keep the forwarding long url, it should like this `https://3456-2003-c7-3713-91c2-3482-6209-8dd2-829c.ngrok-free.app`.
```
ngrok http 4141
```
- Start `ngrok` with the below command if you install `ngrok` with manual download (ensure you are in the directory of the ngrok)
```
./ngrok http 4141
```

## Step 1
- Create a random string character. You can generate one [HERE](https://www.random.org/strings/) ( Keep it also )
- Feel free to choose the length of your choice, example `18`, `24` random string long.

## Step 2
- Create `github token` for `Atlantis` to communicate with `Github`.
  - Watch this 3 mins [Video](https://www.youtube.com/watch?v=m5SChqEi314) on how to create Github token.
  - Please keep the token safe.

## Step 3
- Create the `repository` for your project.
- This `repository` should be where you want to provision your cloud infrastructure from.

## Step 4
- Start `ngrok` by running the below command if you install `ngrok` via brew, copy and keep the forwarding long url, it should like this `https://3456-2003-c7-3713-91c2-3482-6209-8dd2-829c.ngrok-free.app`.
```
ngrok http 4141
```
- Start `ngrok` with the below command if you install `ngrok` with manual download (ensure you are in the directory of the ngrok)
```
./ngrok http 4141
```

## Step 5
- Create a `start.sh` file in any directory of your choice with the below to start your `Atlantis` application
```
#!/bin/bash
URL="Your ngrok url in Step 4"
SECRET="Your random string generated in Step 1"
TOKEN="Your Github Token in Step 2"
USERNAME="Your Github Username"
REPO_ALLOWLIST="github.com/YourGitHubUsername/YourRepositoryName"

atlantis server \
--atlantis-url="$URL" \
--gh-user="$USERNAME" \
--gh-token="$TOKEN" \
--gh-webhook-secret="$SECRET" \
--repo-allowlist="$REPO_ALLOWLIST"
```
- To start Atlantis
  - Run `chmod +x start.sh` on your terminal to make the file executable ( Ensure you are in the directory where the `start.sh` file is ).
  - Run `./start.sh` to start Atlantis.

## Step 6
- Create a `webhook` from that repository
  - Go to the repository `Settings`
  - On the left click `Webhooks`
  - Click `add webhook` on the right
  - set Payload URL to your `ngrok` url with `/events` at the end. Ex. `https://3456-2003-c7-3713-91c2-3482-6209-8dd2-829c.ngrok-free.app/events`
  - double-check you added `/events` to the end of your `ngrok URL`.
  - set Content type to `application/json`.
  - set `Secret` to your random string you generated on `Step 1`.
  - select `Let me select individual events`.
  - check the boxes
    - Pull request reviews
    - Pushes
    - Issue comments
    - Pull requests
    - leave Active checked
    - click Add webhook
 
## Step 7
- Test the set up by creating a pull request of push a terraform configuration to the branch
- Atlantis should kick in to run plan on your branch.


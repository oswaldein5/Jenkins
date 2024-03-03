# Practice-02 - Jenkins with Webhooks using ngrox

## [billing]:Source code as example

## Install ngrok
- `choco install ngrok`: In this case for windows
- `ngrok config add-authtoken <key>`: Run the following command to add your authtoken to the default ngrok.yml

## Deploy your app online
- `ngrok http http://localhost:8080`: in this case for jenkins

## Go to website github:repo and add the webhook
- `https://github.com/oswaldein5/Jenkins/settings/hooks`: With url provided for ngrok + "/github-webhook/"

## It should be something like this
- `https://a0e8-2800-bf0-81ed-f51-a859-964d-1542-e052.ngrok-free.app/github-webhook/`

## Create new branch and move/add/commit/push finally testing github-webhook
- `git branch feature/addtest main`: Add new branch
- `git checkout feature/addtest`: Move to new branch
- `git branch`: Checking
- `git add .`: Add
- `git commit -m "Add new branch"`: Commit
- `git push -u origin feature/addtest`: Push to new branch

## Testing 
- `POST /github-webhook/ 200 OK`: Test result

## Go to Jenkins

- `http://localhost:8080/manage/configure`: [option]: Add GitHub Server
- Choose `Secret text` in credentials and put `github token` [only works with token]
- `Apply` and `Save`
- Create new view `webhooks-pipeline` as `freestyle project` 
- Check the option `GitHub project` and enter url repo github in `Project url` 
- In this case: https://github.com/oswaldein5/Jenkins
- Go to `Source Code Management` and select `Git`
- In `Repositories/Repository URL` enter `https://github.com/oswaldein5/Jenkins.git`
- Enter credentials
- Go to `Branch Specifier (blank for 'any')`: enter `origin/feature**` 
	- ** Check which branch that triggers the pipeline
- Go to `Build Triggers` and check the option `GitHub hook trigger for GITScm polling`
- Go to `Build Steps` and choose the option `Invoke top-level Maven targets`
- In `Goal`s enter `clean install` then in `Advance\POM` enter path `Practice-02/billing/pom.xml`
- `Apply` and `Save`

## Go to terminal (local project: Jenkins/Practice-02)
- Modify test java `\\billing\src\test\java\com\paymentchain\billing`
- `git add .`: Add in billing path
- `git commit -m "Add test"`: Commit
- `git push -u origin feature/addtest`: Push to new branch

## Go to Jenkins
- Check pipeline `webhooks-pipeline`

## Finaly merge everything in github and delete locally branch
`git branch -d feature/addtest`: Delete feature/addtest

---
# Practice-03 - Jenkins CI with JUnit test and Slack Notifications

## [billing+test]:Source code as example

## Create new branch and move/add/commit/push
- `git branch feature/addtest main`: Add new branch
- `git switch feature/addtest`: Move to new branch
- `git branch`: Checking
- Adding Java Test in src Apps, in this case (billing)

## Go to Jenkins

- `http://localhost:8080/manage/configure`: [option]: Add GitHub Server
- Choose `Secret text` in credentials and put `github token` [only works with token]
- `Apply` and `Save`
- Create new view `pipeline_CI_test` as `freestyle project` 
- Check the option `GitHub project` and enter url repo github in `Project url` 
- In this case: `https://github.com/user/repo.git`
- Go to `Source Code Management` and select `Git`
- In `Repositories/Repository URL` enter `https://[token|secrettext]@github.com/user/repo.git`
- Go to `Branch Specifier (blank for 'any')`: enter `origin/feature**` 
	- ** Check which branch that triggers the pipeline
- Go to `Additional Behaviours` in `Add` select the option `Custom user name/e-mail address`
- Enter user.name `jenkins` and enter user.email `email.example.com`
- Go to `Build Steps` and choose the option `Invoke top-level Maven targets`
- In `Goals` enter `clean install` then in `Advance\POM` enter path `Practice-03/billing/pom.xml`
- Go to `Build Steps` and choose the option `Execute shell`
- In `Command` enter the following cmds:
	- git branch
	- git switch main
	- git merge origin/feature/addtest
- Go to `Post-build Actions` and choose the option `Git Publisher`
- Check the option `Push Only If Build Succeeds`: in this case if `clean install`.result is OK then push
- Go to `Post-build Actions` and choose the option `Publish JUnit test result report`
- In the `Test report XMLs`: enter path `Practice-03/billing/target/surefire-reports/*.xml`
- Go to `Branches` then click `Add Branch`
- In `Branches` `Branch to push` enter `main`
 - In `Branches` `Target remote name` enter `origin`
- `Apply` and `Save`

## Go to terminal (local project: Jenkins/Practice-03)
- `git branch`: Checking
- `git add .`: Adding all changed files in Practice-03 for this lab
- `git commit -m "Add integrating Java test"`: Commit
- `git push -u origin feature/addtest`: Push to new branch

## Checking new changes in Github repo
- Execute Pull Request

## Go to Jenkins
- Check pipeline `pipeline_CI_test`
- The pipeline should have done the merge

##

##

---

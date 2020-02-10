# gitlab_runner_study
This is a web to record my GitLab-CI research.

## Introduction
https://about.gitlab.com/stages-devops-lifecycle/continuous-integration/

## Required
 - Add a `.gitlab-ci.yml` file to your repository’s root directory.
 - Install and configure GitLab-runners.
 
## What is `.gitalab-ci.yml` file?
The `.gitlab-ci.yml` file is where we configure what CI does with our project. It lives in the root of the repo.<br>
On any push to the repo, GitLab will look for the gitlab-ci ymal file and start jobs on Runners.<br/>

## How does a Pipeline work?
![](https://github.com/cassieliuxy/gitlab_runner_study/blob/master/images/Pipeline.png)  
  Each stage can have many jobs.<br>
  Jobs of the same stage are run in parallel.<br/>
  If any of the previous job fails, the commit is marked as failed and no jobs of further stage are executed.

## Install GitLab Runner:
*1. Run Docker and pull the latest image:
```Bash
docker pull gitlab/gitlab-runner
```
*2. Start the docker gitlab-runner: (https://docs.gitlab.com/runner/install/docker.html)
```Bash
docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest
```
*3. Check the image:
```Bash
docker ps
```
*4. Register a runner:
 * Go to: `YourProject/Settings/CI|CD/Runners Settings` Find the information of Specific Runners of Shared Runners
 * Command Line:
 ```Bash
 docker exec -it gitlab-runner gitlab-runner register
 ```
 - Enter the URL and token from the runner information.
 - Setup the tags. The tags will be used to configure the runner in `.gitlab-ci.yml`.
 - Configure the description, executor and default image.
*5. Refresh `YourProject/Settings/CI|CD/Runners Settings` to update the runners.

### Reference:
https://about.gitlab.com/stages-devops-lifecycle/continuous-integration/

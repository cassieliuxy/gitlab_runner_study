# GitLab-CI Study
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
  If any of the previous job fails, the commit is marked as failed and no jobs of further stage are executed.<br>
  If anything goes wrong, you can easily roll back all the changes.<br/>

## Install a GitLab Runner:
1. Run Docker and pull the latest image:
```Bash
docker pull gitlab/gitlab-runner
```
2. Start the docker gitlab-runner: (https://docs.gitlab.com/runner/install/docker.html)
```Bash
docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest
```
3. Check the image:
```Bash
docker ps
```
4. Register a runner:
  * Go to: `YourProject/Settings/CI|CD/Runners Settings` Find the information of Specific Runners of Shared Runners
  ![](https://github.com/cassieliuxy/gitlab_runner_study/blob/master/images/Runner_Settings.png) 
  * Command Line:
 ```Bash
 docker exec -it gitlab-runner gitlab-runner register
 ```
   * Enter the URL and token from the runner information.
   * Setup the tags. The tags will be used to configure the runner in `.gitlab-ci.yml`.
   * Configure the description, executor and default image.
5. Refresh `YourProject/Settings/CI|CD/Runners Settings` to update the runners.

## Create a `.gitalab-ci.yml` file:
Examples:
```YMAL
image: ubuntu: 18.04

stages:
  - build
  - test
  
build_job:
  stage: build
  script:
    - echo BUILD
  tags:
    - build

test_job:
  stage: test
  script:
    - echo TEST
    - echo $CI_COMMIT_SHA
  tags:
    - test
```
More information about `.gitalab-ci.yml` file: https://docs.gitlab.com/ee/ci/quick_start/README.html

## Pipelines:
Go to `YourProject/CI|CD/Pipelines`.
![](https://github.com/cassieliuxy/gitlab_runner_study/blob/master/images/Jobs.png) 
It shows the pipeline. When you click the Pipeline number, more information will be shown.
![](https://github.com/cassieliuxy/gitlab_runner_study/blob/master/images/Pipeline_Details.png) <br>
When you click the jobs on the pipeline, you can see more details.<br/>


### Reference:
 - https://about.gitlab.com/stages-devops-lifecycle/continuous-integration/
 - https://docs.gitlab.com/runner/install/docker.html
 - https://docs.gitlab.com/ee/ci/quick_start/README.html

#### Author: Xiaoyan Liu (https://github.com/cassieliuxy/gitlab_runner_study)

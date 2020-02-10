# gitlab_runner_study
This is a web to record my GitLab-CI research.

## Introduction
https://about.gitlab.com/stages-devops-lifecycle/continuous-integration/

## Required
 - Add a `.gitlab-ci.yml` file to your repository’s root directory.
 - Install and configure GitLab-runners.

## How does a Pipeline work?
![](https://github.com/cassieliuxy/gitlab_runner_study/blob/master/images/Pipeline.png)  
  Each stage can have many jobs.<br>
  Jobs of the same stage are run in parallel.<br/>
  If any of the previous job fails, the commit is marked as failed and no jobs of further stage are executed.


### Reference:
https://about.gitlab.com/stages-devops-lifecycle/continuous-integration/

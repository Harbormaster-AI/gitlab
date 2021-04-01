# Harbormaster Project Generator For GitLab

![alt text](http://harbormaster.ai/wp-content/uploads/2021/03/captain_harbormaster-e1617238219491.png)

The contained GitLab configuration file (_.gitlab-ci.yml_) is a simple, yet powerful way to leverage Harbormaster and GitLab to automate the generation of an MVP-quality projects built on, tested, contained and deployed through your GitLab CI/CD pipeline.

This repository also contains [sample Harbormaster project generation YAML files](https://gitlab.com/Harbormaster-AI/gitlab/blob/master/samples/yamls/project.as.code/).  These instructions will reference the Django project file (_django-project-as-code.yaml_)

To take a quick test drive, follow the instructions in the *Quick Start* section or skip to the _Step-By-Step_ section to generate an application using more customized inputs.

## Quick Start

Use this section to make the least amount of changes to see Harbormaster project generation in action.  

1.) Git Clone this project in one of two ways:

` SSH - git@gitlab.com:Harbormaster-AI/gitlab.git`
` HTTPS - https://gitlab.com/Harbormaster-AI/gitlab.git`

2.) Edit the _git_ section of `/samples/yamls/project.as.code/django-project-as-code.yml` to set your GitLab username and password.

3.) Create a GitLab repository by the name of _django_repo_.

4.) Create a GitLab pipeline that is connected to the GitLab _django_repo_

5.) Commit your changes to this project to the _django_repo_ and observe the GitLab pipeline status.

6.) Once the job in the pipeline is complete, check its status. A project will have been generated using a default model and a Django tech stack.

The project will eventually be built and tested with results as below:

![alt text](http://harbormaster.ai/wp-content/uploads/2021/04/gitlab-app-build-running-results.png)


# Step-By-Step Project Generation

## Step 1 - Clone This Project
Clone this project in one of two ways:

` SSH - git@gitlab.com:Harbormaster-AI/gitlab.git`
` HTTPS - https://gitlab.com/Harbormaster-AI/gitlab.git`

## Step 2 - Make Changes

#### API_TOKEN

An api_token is required to initialize a unique session with the Harbormaster SaaS back-end.  The one provided as default is safe to 
use as a GitLab user.  However, if you prefer, assign your API token, which is available by logging into the [Harbormaster SaaS](platform.harbormaster.ai).

`API_TOKEN: "CBc10800RKddRGQh"`

#### PROJECT\_YAML\_FILE:

This YAML file contains the directives required to generate a project including:
- model identifier (by name, id or file_path)
- tech stack (by name or id), 
- application options (name, description, author, etc..)
- GitLab repo settings, 
- Docker settings
- and more.... 

See an example [here](https://github.com/Harbormaster-AI/gitlab/blob/main/samples/yamls/project.as.code/django-project-as-code.yml)


`PROJECT_YAML_FILE: "samples/yamls/project.as.code/django-project-as-code.yml"`

#### GitLab Credentials
Modify the git: section of the a _PROJECT_YAML_FILE_ (e.g. django-project-as-code.yml) to assign your GitLab credentials

##### AWS Credentials
Note: If using one of the AWS Lambda stacks, you will have to assign the access key and secret key as project level environment variables.  See [https://gitlab.com/help/ci/variables/README#variables](https://gitlab.com/help/ci/variables/README#variables) for more details. Be sure to name the accesskey USER\_AWS\_ACCESSKEY and name the secretkey USER\_AWS\_SECRETKEY.  Equally important, 
make sure you have the correct policies assigned for the related user (_AWSCodeDeployRoleForLambda, AWSLambdaExecute, AWSLambdaRole_, etc..)

## Step 3 - Create a Repository For Generated Project files
Create a GitLab project repository (Repo A) for the generated project files.  This repository name must be the name you assigned in the GIT section of the _PROJECT_YAML_FILE_ (e.g. django-project-as-code.yml).

## Step 4 - Create a Project For This Cloned Project
Create another GitLab project repository (Repo B) and commit this project to it.  Any name will do.  You are committing the modified _.gitlab-ci.yml_ file along with the _PROJECT_YAML_FILE_ discussed above.  Only the _.gitlab-ci.yml_ must be in the root.   

## Step 5 - Commit Your Project
Upon committing this project to Repo B, the _.gitlab-ci.yml_ should begin running within a bound GitLab pipeline. The project is now being generated by Harbormaster.

![alt text](http://harbormaster.ai/wp-content/uploads/2021/04/gitlab-job-running.png)

## Step 6 - Watch Pipeline Execution
Upon completion of Step 5, Harbormaster will commit all generated project files to Repo A.  This should cause a GitLab pipeline to run the generated _.gitlab-ci.yml_ file.  The generated project is now being built and tested.

![alt text](http://harbormaster.ai/wp-content/uploads/2021/04/gitlab-app-build-running-results.png)

## Congratulations!
Using the power of GitLab and Harbormaster, you just generated, built, tested, and (optionally) contained an entire application complete with core capabilities, build file, CI/CD config, and much more....

Best of luck in completing the application!



# github-action-dev-build
Build individual HPCC-Platform Project Artifacts with Github Actions for unit testing and integration testing of any docs code changes. 
This respository is a means to build specified Github branches/tags/commits etc

This repository contains the sauce for building HPCC-Platform using GitHub Actions. 
To enable the github-action-builds to build from your git REF 
 1. Clone this repository.
 2. Customize the build-docs.yaml
 3. Build on Push or manual trigger
 4. Retrieve and Review Artifacts

# Customization
In order to get this build action to work for your individual repository. 
Clone this repository to your git repositories 

## prerequisites: 
You must have a dockerhub account to build the virtual machine for building. Note your dockerhub account username and password. 
Your Docker username is the same username that you use when you log into Docker  (docker.com or docker.io).

## Setting Up Repository Secrets
You need to set up the secrets on your (clone) of the GitHub action-build repository. 
(For example: github.com/yourREPO/github-action-dev-build) That's your fork of the repository. 
1. Choose the settings tab from the 2nd row on the page (https://github.com/yourREPO/github-action-dev-build/settings) 
2. Click on Settings.
3. Along the left hand menu on the settings page, select the **secrets and variables** under the security section
4. Click on **Actions** under that submenu. 
5. Press the  **New Repository Secret** button
6. Enter **DOCKERHUB_USERNAME** in the Name field.
7. Enter your Dockerhub account username into the Secret field.
8. Press **Add Secret** button to create and store that secret
9. Press the  **New Repository Secret** button
10. Enter **DOCKERHUB_PASSWORD** in the Name field.
11. Enter your Dockerhub account password into the Secret field.
12. Press **Add Secret** button to create and store that secret

# Configuring Building from your Repo
To configure for builds you need to tell it what you want to build, and when. These are the steps in order to do that. first you will need to get your community ref value for the build script. The community ref value referred to is the Git REF value for the git object -commit, branch, tag, etc. that you want to build. For example if you wanted to test your branch that you just created, you need to get that value for the community REF. 

## Get the REF value
To get the community REF value, using github cli enter :
     ```
     git show-ref --head
     ```
Alternatively you can filter on branch name, if you had ABCBranch you could use 
     ```
     git show-ref --head | grep ABC
     ```
Copy the entire string that compromises the community REF for the desired branch/commit

>>   SAVE THAT INFO to input in to the build-docs.yaml file on line 16
     it must be an exact match.

## Configure the build-docs.yaml script
Navigate to the base of your github-actions-build repository and locate the .github/workflows folder 
(?Think tab navigation is possible https://github.com/yourname/github-action-dev-build/tree/main/.github/workflows)
edit the _build-docs.yaml_ file there: 
   1. (OPTIONAL) on lines 7-9 comment out workflow_dispatch and uncomment #push to enable build on push 
        NOTE: matter of preference if you want to build every time you push or only build when you specificy manually
   2. Navigate to around line 16 (at time of this write up)
       Find =>  COMMUNITY_REF:  <GIT REF>
   3. Replace <GIT REF> with your REF sting you copied earlier from the branch/tag you wish to build
   4. OPTIONALLY you can scroll down to approximately line 163 and change the name of the artifacts file produced
   5. Need to save the build-docs.yaml file then commit to your main

## Build
This will now build the branch/tag/commit you specified in the Community <REF> every single time you push

Go to the Actions Tab on the github-actions-build repo

In the panel on the left it lists all workflows - using this repo it only builds the Build Documentation Workflow
   1. Select the Build Documentaton Workflow 
      It displays the workflow runs
  2.  Select the workflow run to inspect
  3.  On that selected workflow run page on the right side scroll down and locate the Artifacts produced by the run
  4.  Download the artifacts or share the link to Artifacts page with anyone who has access to your github repository (public?)    

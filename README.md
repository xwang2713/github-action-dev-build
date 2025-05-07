# github-action-dev-build
Build individual HPCC-Platform Project Artifacts with Github Actions for unit testing and integration testing of any docs code changes. 
This respository is a means to build specified Github branches/tags/commits etc

This repository contains the sauce for building HPCC-Platform using GitHub Actions. 
To enable the github-action-builds to build from your git REF 
 1. Clone this repository.
 2. Customize the build-docs.yaml
 3. Build on Push or manual trigger
 4. Retrieve and Review Artifacts

## Customization
In order to get this build action to work for your individual repository. 
Clone this repository to your git repositories 
*Alternately* it may be easier to fork the repo instead of cloning 

### prerequisites: 
You must have a dockerhub account to build the virtual machine for building. Note your dockerhub account username and password. 
Your Docker username is the same username that you use when you log into Docker  (docker.com or docker.io).

### Setting Up Repository Secrets
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

## Configuring Building from your Repo
To configure for builds you need to tell it what you want to build, and when. These are the steps in order to do that. first you will need to get your community ref value for the build script. The community ref value referred to is the Git REF value for the git object -commit, branch, tag, etc. that you want to build. For example if you wanted to test your branch that you just created, you need to get that value for the community REF. 

### Get the REF value
To get the community REF value, using github cli enter :
     ```
     git show-ref --head
     ```
Alternatively you can filter on branch name, if you had ABCBranch you could use 
     ```
     git show-ref --head | grep ABC
     ```
  Another place to find your REF (or SHA) is to go to Github.com 
  If you pushed your file - on the "Open a Pull Request" Page it displays the Git REF (aka SHA)
  There is also an button next to the REF "Copy the full SHA" - does this next bit in one click
### Get the REF From GitHub
To get the REF: on Github site click on the commit and it is on the top right of the commit 

Copy the entire string that compromises the community REF for the desired branch/commit

>>   SAVE THAT INFO to input in to the build-docs.yaml file on line 16
     it must be an exact match to the branch/commit that you want to build.

### Configure the build-docs.yaml script
Navigate to the base of your github-actions-build repository and locate the .github/workflows folder 
(?Think tab navigation is possible https://github.com/yourname/github-action-dev-build/tree/main/.github/workflows)
edit the _build-docs.yaml_ file there: 
   1. (OPTIONAL) on lines 7-9 comment out workflow_dispatch and uncomment #push to enable build on push 
        NOTE: matter of preference if you want to build every time you push or only build when you specificy manually
   2. Navigate to around line 16 (at time of this write up)
       Find =>  COMMUNITY_REF:  <GIT REF>
   3. Replace <GIT REF> with your REF sting you copied earlier from the branch/tag you wish to build
   4. OPTIONALLY you can scroll down to approximately line 163 and change the name of the artifacts file produced
   5. Need to save the build-docs.yaml file then commit (to your 'main')

## Build Other Projects

Build individual HPCC-Platform Project with Github Action
To use this clone this repo to your Github account, pick a github action script under .github/workflows/
Replace the <GIT REF> for the HPCC-Platform/LN/ECLIDE branch. You also can replace GITHUB_ACCOUNT if users
want to build with other Github account.
Users can modify the CMake options as they wish

Requirement: following Michael's instruction to create SECRETS.

To trigger a build automatically uncommts push and disable workflow_dispatch:
```code
on:
  #workflow_dispatch:
  push:
```

Commit the change and submit this branch to start the build:
If you don't set "push" you can pick a script from .github/workflow/ and manually run the workflow Github Action
```console
git add <workspaces>/<script>
git commit
git push origin +master
```
The output packages should be in artifact of the action


### CE Platform
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT REF> in .github/workflows/build-ce-platform.yml
```code
COMMUNITY_REF:  <GIT REF>
```
The default artifact file name: CE-HPCC-Platform-<os>.zip

### CE Plugins
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT REF> in .github/workflows/build-ce-plugins.yml
```code
COMMUNITY_REF:  <GIT REF>
```
The default artifact file name: CE-HPCC-Plugins-<os>.zip

### LN Platform and Clienttools
Get LN and Platform git reference
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT CE REF> and <GIT LN REF> in .github/workflows/build-ln-platform.yml
```code
COMMUNITY_REF:  <GIT CE REF>
LN_REF:  <GIT LN REF>
```
The default artifact file name: LN-Packages-<os>.zip

### Windows and OSX Community/LN Clienttools
Get LN and Platform git reference
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT CE REF> and <GIT LN REF> in .github/workflows/build-win-osx.yml
```code
COMMUNITY_REF:  <GIT CE REF>
LN_REF:  <GIT LN REF>
```
The default artifact file names: WinOSX-Clienttools.zip and WinOSX-LN-Clienttools.zip

### ECLIDE Build
Get LN and Platform git reference
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT CE REF> and <GIT LN REF> in .github/workflows/build-ide.yml
```code
COMMUNITY_REF:  <GIT CE REF>
LN_REF:  <GIT LN REF>
```
The default artifact file names: ECLIDE.zip


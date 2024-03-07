# github-action-dev-build
Build individual HPCC-Platform Project Artifacts with Github Action
This repository contains the sauce for building HPCC-Platform using GitHub Actions. 
Clone this repository and customize for your GitHub repository. 
# Customization
In order to get this build action to work for your individual repository. 
## prerequisites: 
  1. input your *dockerusername* and *dockerpassword* for your docker.io credentials into github secrets.
  2. get your community ref

            a. on github cli :
          ```
     git show-ref --head
     ```

           b. get that head
                       info - should be a long string
     SAVE THAT INFO to input in to the build-docs.yaml file on line 16
     it must be an exact match.

## Actions Set-Up 

1. Clone the github-action-dev-build repository

2. Go to .github/workflows

3. Edit build-docs.yaml:

   a. lines 7-9 comment out workflow_dispatch and uncomment #push to enable build on push

   b. around line 16 you add your community ref you got from  above:
        Find =>  COMMUNITY_REF:  <GIT REF>

   And replce <GIT REF> with your ReF sting you copied 

   c. Need to save the file then commit to your master
      
6. make a push to the repo - it 'should' build

7. Retrieve Artifacts (Monitor Job) from the GitHub Actions tab    


## Original Developer Notes
Pick a workflow script and uncommts push and disable workflow_dispatch:

```code
on:
  #workflow_dispatch:
  push:
```
Update <GIT_REF> and related settings following each build case

To trigger the build:
```console
git add <workspaces>/<script>
git commit
git push origin +master
```
The output packages should be in artifact of the action

## Obtaining your GIT REF 
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT REF> in .github/workflows/build-docs.yml
```code
COMMUNITY_REF:  <GIT REF>
```
The default artifact file name: html-help-documents.zip


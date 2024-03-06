# github-action-dev-build
Build individual HPCC-Platform Project Artifacts with Github Action

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

## Documentation
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT REF> in .github/workflows/build-docs.yml
```code
COMMUNITY_REF:  <GIT REF>
```
The default artifact file name: html-help-documents.zip



# Customization
In order to get this build action to work for your individual repository. 
## prerequisite: 
  1. input your dockerusername and dockerpassword for your docker.io credentials into your github secrets.
  2. get your community ref
       a. on github cli :
          ```
     git show-ref --head
     ```
       b. get that head
                       info - should be a long string
     SAVE THAT INFO to input in the build-docs.yaml file on line 16
     that must be an exact match. 

## steps
1. Clone this repository
2. Go to .github/workflows
3. Edit build-docs.yaml:
   a. lines 7-9 comment out workflow_dispatch and uncomment #push to enable build on push
   b. somewhere around line 16 you add your community ref you got from  above 
   c. maybe that is it
   
6. make a push to the repo - it 'should' build
   

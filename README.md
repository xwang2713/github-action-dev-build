# github-action-dev-build

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

## Documentation
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT REF> in .github/workflows/build-docs.yml
```code
COMMUNITY_REF:  <GIT REF>
```
The default artifact file name: html-help-documents.zip

## CE Platform
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT REF> in .github/workflows/build-ce-platform.yml
```code
COMMUNITY_REF:  <GIT REF>
```
The default artifact file name: CE-HPCC-Platform-<os>.zip

## CE Plugins
```console
git show-ref --head <branch name>
```
Get the first line first column and replace <GIT REF> in .github/workflows/build-ce-plugins.yml
```code
COMMUNITY_REF:  <GIT REF>
```
The default artifact file name: CE-HPCC-Plugins-<os>.zip

## LN Platform and Clienttools
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

## Windows and OSX Community/LN Clienttools
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

## ECLIDE Build
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

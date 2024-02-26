# github-action-dev-build

Build individual HPCC-Platform Project with Github Action

Requirement: following Michael's instruction to create SECRETS.



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
The default artifact file name: LN-Packages-<os>.mzip



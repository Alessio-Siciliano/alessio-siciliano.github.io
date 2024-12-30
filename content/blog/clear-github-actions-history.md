---
title: "How to Clear GitHub Actions History in a Few Simple Steps"
date: 2024-12-30
authors:
  - name: Alessio Siciliano
    link: https://github.com/Alessio-Siciliano
    image: https://github.com/Alessio-Siciliano/imfing.png
tags:
  - Github
  - Git
  - Guide
  - Repository Cleanup
  - GitHub Actions
  - Workflow Management
  - Repository Cleanup
  - CI/CD
  - Automation
  - Development Tools
excludeSearch: false
comments: true

---

GitHub Actions is a powerful tool for automating workflows, but sometimes you may need to clear its history. Whether it’s for privacy, to free up storage, or to maintain a clean repository, the process is straightforward. Here’s a step-by-step guide to achieve this.

## Introduction

GitHub Actions helps automate workflows, but there are times when you might want to clear its history, whether for privacy, debugging, or to maintain a clean repository. This guide will show you how to do this by creating and running a simple workflow.

This process doesn’t delete logs from the past permanently stored by GitHub, but it helps replace them with a clean slate.

## Why reset a Repository?
1. **Privacy**: Remove sensitive or unnecessary information.
2. **Debugging**: Start fresh to test new workflows.
3. **Organized Repository**: Keep your Actions tab tidy and focused.

## Steps to Reset a Git Repository
Follow these steps to clear Github Action history:

{{% steps %}}

### Create API token
Create an API token with `Repository access: Actions: Read and write` and store the key.

### Create a Bash Script
Start by creating a new file called `clear_history.sh` in your local repository directory. Add the following content to it:
```bash
#!/bin/bash
OWNER="--USER_NAME--" #EDIT
REPO="--REPO_NAME--" #EDIT
TOKEN="--MY_TOKEN--" #EDIT

runs=$(curl -s -H "Authorization: token $TOKEN" \
  "https://api.github.com/repos/$OWNER/$REPO/actions/runs" | grep '"id":' | awk '{print $2}' | tr -d ',')

for run_id in $runs; do
  echo "Deleting run ID: $run_id"
  curl -X DELETE -H "Authorization: token $TOKEN" \
    "https://api.github.com/repos/$OWNER/$REPO/actions/runs/$run_id"
done
```
Edit the three variables with your data and the key created in the previous step.

### Execute script
Execute the script from terminal:
```bash
./clear_history.sh
```
{{% /steps %}}

## Conclusion
Clearing GitHub Actions history is a simple yet effective way to maintain a clean and organized repository. By following this guide and using a straightforward Bash script, you can reset your workflows and ensure your repository remains tidy and efficient. **Remember to handle your GitHub tokens securely and revoke them when no longer needed**.
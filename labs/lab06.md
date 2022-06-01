# 6 - Automate GitHub Releases
In this lab you will automate GitHub Releases using the Release Drafter action.
> Duration: 15-20 minutes

References:
- [About releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)
- [Automatically generated release notes](https://docs.github.com/en/repositories/releasing-projects-on-github/automatically-generated-release-notes)
- [GitHub Action - Release Drafter](https://github.com/marketplace/actions/release-drafter)
- [GITHUB_TOKEN - permissions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#permissions)

## 6.1 Automate GitHub Releases using Release Drafter GitHub Action

1. Navigate to the action repository [release-drafter](https://github.com/release-drafter/release-drafter) and read the documentation on how to use the action
2. Add a new workflow file `.github/workflows/release-drafter.yml` to your repository
3. Copy and paste the following content to the newly created file:
```YAML
name: Release Drafter

on:
  push:
    branches:
      - main

# Comment out the 2 lines if the permissions for the GITHUB_TOKEN is read and write and you get an workflow runtime error
permissions:
  contents: write

jobs:
  update_release_draft:
    runs-on: ubuntu-latest
    steps:
      - uses: release-drafter/release-drafter@v5
        with:
           config-name: release-drafter.yml
           disable-autolabeler: true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
4. Commit the changes into a new `feature/lab06` branch
5. Using the same `feature/lab06` branch, add a new configuration file `.github/release-drafter.yml`
6. Copy and paste the following content to the newly created file:
```YAML
template: |
  ## What’s Changed

  $CHANGES
```
7. Commit the changes into the `feature/lab06` branch
8. Open a new pull request and merge the `feature/lab06` branch into the `main` branch
9. Go to `Actions` and see the details of your `Release Drafter` workflow 
10. After the workflow completed, navigate to the `Releases` page to see your `v0.1.0` draft release
11. Open the configuration file [release-drafter.yml](/.github/release-drafter.yml)
12. Copy and paste the more complicate configuration content:
```YAML
name-template: 'v$RESOLVED_VERSION 🌈'
tag-template: 'v$RESOLVED_VERSION'
categories:
  - title: '🚀 Features'
    labels:
      - 'feature'
      - 'enhancement'
  - title: '🐛 Bug Fixes'
    labels:
      - 'fix'
      - 'bugfix'
      - 'bug'
  - title: '🧰 Maintenance'
    label: 'chore'
change-template: '- $TITLE @$AUTHOR (#$NUMBER)'
change-title-escapes: '\<*_&' # You can add # and @ to disable mentions, and add ` to disable code blocks.
version-resolver:
  major:
    labels:
      - 'major'
  minor:
    labels:
      - 'minor'
  patch:
    labels:
      - 'patch'
  default: patch
template: |
  ## Changes

  $CHANGES
```
13. Commit the changes into a new `feature/lab06` branch
14. Open a new pull request and add the `enhancement` label 
15. Complete the pull request and merge the `feature/lab06` branch into the `main` branch
16. Go to `Actions` and see the details of your `Release Drafter` workflow 
17. After the workflow completed, navigate to the `Releases` page to see you `v0.1.0` draft release updated
18. Edit the `v0.1.0` draft release and publish your first release
19. Open the configuration file [release-drafter.yml](/.github/release-drafter.yml) 
20. Copy and paste the following content into the `categories` configuration:
```YAML
  - title: '⬆️ Dependencies'
    collapse-after: 3
    labels:
      - 'dependencies'
```
21. Commit the changes into a new `feature/lab06` branch
22. Open a new pull request and add the `bug` label 
23. Complete the pull request and merge the `feature/lab06` branch into the `main` branch
24. Go to `Actions` and see the details of your `Release Drafter` workflow 
25. After the workflow completed, navigate to the `Releases` page to see your new `v0.1.1` draft release
26. _(Optional)_ Enable the `autolabeler` option of the Release Drafter and configure it to add automatically a label into a pull request. See details [Autolabeler](https://github.com/release-drafter/release-drafter#autolabeler)

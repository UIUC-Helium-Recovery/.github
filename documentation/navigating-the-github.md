# Navigating the UIUC Helium Recovery Organziation GitHub

- **Author**: Luke Marren
- **Recent Updates**:
  - Date: 6-2-25
  - Maintainer(s): Luke Marren

## Table of Contents

- [GitHub Repository Introduction](#github-repository-introduction)
    - [.github](#github)
    - [RPis](#rpis)
    - [medusa](#medusa)
- [Project Management](#project-management)
    - [Our GitHub Project](#our-github-project)
    - [Issue Workflow](#issue-workflow)

## GitHub Repository Introduction
There are three Git repositories hosted on GitHub under the perview of the UIUC Helium Recovery Organization. They are:

### .github

- **Quick Summary**: This is a special repo that GitHub uses to automatically create a README file for the organization.
- The current org README is located [here](github.com/UIUC-Helium-Recovery/profile/README.md) and is displayed as the `Helium Recovery Handbook` on the org's homepage.
- Also inside this repo is documentation written in markdown (e.g., `navigating-the-github.md`). It's easier to write quick documentation in markdown than on the box, especially if you want to include code blocks.

### RPis

- **Quick Summary**: This repo is used to backup and help with Git workflows for the main analysis Python and Shell files on the Raspberry Pis.
- **Branches**: RPis is split into two primary branches for development:
    - `loomis434`: the 'main', default branch, which is connected to and backs up code in the `/home/pi/medusa/` folder on Sloan's Pi.
    - `dev`: the child of `loomis434` that's connected to the `/home/pi/medusa/` folder on John's Pi. We test and review all code to be deployed to Sloan's Pi (our designated main analysis Pi) using this branch
    - `"feature"` branches:
        When we're working on new features to add to `loomis434`, we branch off of it and create a new feature branch to later be merged with `dev` and then, when we're sure our code works, with `loomis434`
### medusa

 - **Quick Summary**: his repo is used to backup and help with Git workflows for the [helium recovery website](heliumrecovery.web.illinois.edu).
 - **Branches**: medusa is split into two primary branches for development:
     - `cPanel`: the 'main', default branch, which is connected to and backs up code in the `/public_html/` folder on cPanel.
     - `dev`: the child of `cPanel`. This performs the same function as the `dev` branch in `RPis` but for the website's development.
     - `"feature"` branches:
        - Feature branches are used the same way as in `RPis`, replacing `loomis434` with `cPanel`.

## Project Management

### Our GitHub Project

In addition to our repos, we have an associated project called the `Helium Recovery Project` to help us communicate with each other over GitHub for code reviews on issues, pull-requests, and other project management duties.

### Issue Workflow
Each time there's a bug in our code, need for documentation, new feature, ... , etc., we can create a new issue under the `issues` tab in the `RPis` or `medusa` repos. Make sure to:

- classify the issue correctly (e.g., as a bug, documentation, enhancement, ... , etc.),
- assign someone (such as yourself) to the issue,
- link the issue with with the `Helium Recovery Project`,
- and, **most importantly**, create a new branch off the repo's main branch for the issue (this is done after issue creation). This is so that you don't accidentally edit the dev/main branches unintendedly or mess with someone else's code.

When you've sent a pull request, everyone's reviewed and approved of your changes, and you've merged your feature branch to the dev branch and then the main branch, be sure to close the issue.

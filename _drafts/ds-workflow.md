
layout: post
title: My Opinionated Guide on Data Science Project Best Practices
---

For those that don't know, I am a Senior Data Scientist at IBM (specifically in GBS, IBM's consulting arm). As a Sr. Data Scientist, I am tasked with leading small teams of data scientists to delivery on client engagements which are generally around 6 weeks long each. Surprisingly, there is no established set of best practices for technical leads to follow within IBM, so I have had to hone my own process over the years. Since I've had to learn lots of things the hard way, I thought I would write down my process here for my own reference and for anyone else to take and use themselves.

With that said, I want to mention some caveats:
1. There may be better ways to do certain things that I don't know about. Please leave suggestions in the comments!
2. Every project is different. This is a rough guide for myself and others and should be treated as such.
3. My expertise is in data science, which has a distinctly different project structure from traditional SE. There will be some crossover in this list, but it will be tailored towards data science (hell, it's in the title).

## Starting out the Project
Brief Intro. TODO

### Directory Structure
cookiecutter. TODO

### Write Minimal `setup.py` File
copy and paste from project. TODO

### Install Universally Needed Dependencies and Populate Intial `environment.yml` or `requirements.txt` file
numpy, pandas, sklearn, mypy, flake8, pytest, nbstripout, pre-commit, etc. TODO

### Set up Data Infrastructure
Database instead of flat files. TODO

### Create `.pre-commit-hooks.yaml` File
copy and paste. talk about installing precommit, etc. Make sure you are on pre-commit 2.6 in order to properly identify ipynb files.

### Set up CI
TODO

## Ways of working
TODO

### Branching
TODO

### Testing
Bake into CI. Force coverage.

### Enforce use of flake8 and mypy
TODO

### Use github projects / issues for project management
TODO

### Use nbstripout for commiting notebooks to github
incorporate into git hooks!!

### Manage environment variables in local .env folders
TODO

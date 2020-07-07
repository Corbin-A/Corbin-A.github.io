layout: post
title: My Opinionated Guide on Data Science Project Best Practices
---

For those that don't know, I am a Senior Data Scientist at IBM (specifically in GBS, IBM's consulting arm). As a Sr. Data Scientist, I am tasked with leading small teams of data scientists to delivery on client engagements which are generally around 6 weeks long each. Surprisingly, there is no established set of best practices for technical leads to follow within IBM, so I have had to hone my own process over the years. Since I've had to learn lots of things the hard way, I thought I would write down my process here for my own reference and for anyone else to take and use themselves.

With that said, I want to mention some caveats:
1. There are almost certainly better ways to do certain things that I don't know about. Please leave suggestions in the comments!
2. Every project is different. This is a rough guide for myself and others and should be treated as such.
3. My expertise is in data science, which has a distinctly different project structure from traditional SE. There will be some crossover in this list, but it will be tailored towards data science (hell, it's in the title).

I am splitting this up into overarching sections: 1) ways of working; and 2) starting out the project. I think everyone, including IC would benefit from the former, while the latter will be tailored more towards technical leads as they start out a new project.

## Ways of working
In this section I'm going to discuss project workflow as well as some structures and practices that I recommend when working on a project. If you have experience with SE teams already, some of these may seem obvious, but the DS world is surprisingly removed from many of the best practices in SE (the deserved vs. merely percieved differences between DS and SE is a topic way too big for this guide). The following are roughly ordered in order of priority.

### General Flow
This is probably a pretty personal thing and it is hard to make hard-and-fast rules around it, but I generally try to keep my DS work structured in the following flow: 1) Exploratory Data Analysis (EDA); 2) Data Prep; 3) Feature Engineering; 4) Model Training; and 5) Model Predicting. For EDA, I keep this in notebook form only, with inline plots and prose around some of my observations. For everything else I start my experimentation in notebooks and when things start solidifying, I transfer the code into python modules, write unit tests, etc. Do note, however, that this [is not a universally accepted workflow](https://www.youtube.com/watch?v=7jiPeIFXb6U) and there are other ways of developing for DS. For instance, Joel Grus (see video link in last sentence) develops only in python modules in his text editor of choice and uses the ipython repl for quick interactivity with his code.

### Branching
When you are working in a team of DS's, you should take advantage of SE collaborative best practices a la git branching. There is a lot of literature on doing this in SE, but not as much for DS specifically, and that's probably because there is a decent amount of crossover. However, one main difference is that the DS workflow often starts in notebooks before migrating code into python scripts. Notebooks are notoriously bad for VC and collaborative programming due to the JSON file structure and experimental nature of notebooks, and I will address these. With that said, here are my recommendations:
1. All active development including notebooks should take place in branches and [merges into master should be restricted to PR's](https://docs.github.com/en/github/administering-a-repository/enabling-branch-restrictions). This will allow for good git commit etiquette of commiting small and often in branches, but ensure by the time that the code is being merged into master it passes relevant CI checks. It also communicates to the team that work is done and can be utilized in their own work.
1. When working on notebooks, use [nbstripout](https://github.com/kynan/nbstripout) to strip all output as well as input / output markers before commiting. See [this video](https://www.youtube.com/watch?v=BEMP4xacrVc) for just how useful this program is for notebook VC. Furthermore, nbstripout can be enforced with pre-commit git hooks, which is discussed in the next section.
1. When working on notebooks, create a "feature branch" while working on a specific notebook. Once work on that notebook is in a state worth sharing with the wider team, then a PR can be submitted to bring it into master.
1. When transitioning from notebooks to python scripts, traditional SE branching best practices can be followed.

### Use git hooks to enforce use of nbstripout, flake8, and mypy
TODO
incorporate into git hooks!!

### Testing
Bake into CI. Force coverage.

### Use github projects / issues for project management
TODO

### Manage environment variables in local .env folders
TODO

### Write README docs in rst instead of md for autodocumentation


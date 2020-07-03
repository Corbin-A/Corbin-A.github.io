
layout: post
title: My Opinionated Guide on Data Science Project Best Practices
---

For those that don't know, I am a Senior Data Scientist at IBM (specifically in GBS, IBM's consulting arm). As a Sr. Data Scientist, I am tasked with leading small teams of data scientists to delivery on client engagements which are generally around 6 weeks long each. Surprisingly, there is no established set of best practices for technical leads to follow within IBM, so I have had to hone my own process over the years.

With that said, I want to mention some caveats:
1. There may be better ways to do certain things that I don't know about. Please leave suggestions in the comments!
2. Every project is different. This is a rough guide for myself and others and should be treated as such.
3. My expertise is in data science, which has a distinctly different project structure from traditional SE. There will be some crossover in this list, but it will be tailored towards data science (hell, it's in the title).








---
I. Directory Structure (from cookiecutter)
II. Flake8 / mypy adherence
III. pytest enforcement (code coverage reqs)
IV. Pre-Commit Hooks
V. Travis
VI. Mode of working (git branches — one branch per notebook. EDA, Data Prep, Feature Engineering, Modeling, Vizualizaitons)
VII. Centralized DB instead of flat CSV files everywhere

---
layout: post
title: Starting a Data Science Project from Scratch
---

For those that don't know, I am a Senior Data Scientist at IBM (specifically in GBS, IBM's consulting arm). As a Sr. DS, I am tasked with leading small teams of data scientists to delivery on client engagements which are generally around 6 - 12 weeks long. As such, I have had to start quite a few distinct DS projects. Surprisingly, there is no established set of best practices for technical leads to follow within IBM, so I have had to hone my own process over the years. Since I've had to learn lots of things the hard way, I thought I would write down my process here for my own reference and for anyone else to take and use themselves.

With that said, I want to mention some caveats:
1. There are almost certainly better ways to do certain things that I don't know about. Please leave suggestions in the comments!
2. Every project is different. This is a rough guide for myself and others and should be treated as such.
3. I code almost exclusively in python for Data Science. I do not know the R ecosystem well enough to give advice on R projects.
4. My expertise is in data science, which has a distinctly different project structure from traditional SE. There will be some crossover in this list, but it will be tailored towards data science (hell, it's in the title).

This page will deal specifically with creating:
1. The overall directory structure
2. An `environment.yml` file seeded with necessary packages
3. A `setup.py` file for easy `pip install -e .`
4. A `.pre-commit-config.yaml` file to enforce nbstripout, flake8 and mypy via pre-commit git hook
5. `tests/` directory and notes around testing in DS projects
6. A `.travis.yml` or other CI recipe file
7. Data infrastructure
8. Getting Started section in README

### Directory structure
This should be flexible to accomidate the needs of the project, but a great starting point can be found at [cookiecutter-datascience](https://github.com/drivendata/cookiecutter-data-science). When I personally start off a project, I remove some of the pre-populated files and get down to the following directory structure:

```
├── .gitignore
│
├── README.rst         <- The top-level README for developers using this project.
│
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default Sphinx project; see sphinx-doc.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
└── <pkg_name>         <- Source code for use in this project.
    ├── __init__.py    <- Makes src a Python module
    │
    ├── data_prep      <- Scripts to download or generate data
    │   └── make_dataset.py
    │
    ├── feat_eng       <- Scripts to turn raw data into features for modeling
    │   └── build_features.py
    │
    ├── models         <- Scripts to train models and then use trained models to make
    │   │                 predictions
    │   ├── predict_model.py
    │   └── train_model.py
    │
    └── visualization  <- Scripts to create exploratory and results oriented visualizations
       └── visualize.py
```
This gets us started, but we need to set up a bit more infrastructure.

### Write minimal `setup.py` file
When your team starts writing `.py` files, they will need to be importing from around the `<pkg_name>` directory. Imports are a major PITA in python if you don't locally pip install the project. To allow for absolute imports, you should create a minimal `setup.py` file such as this:

```python
from setuptools import setup, find_packages

setup(
    name='name-of-project',
    version='0.1.0',
    description='short description of project',
    author='author name',
    author_email='author@email.com',
    url='github pages or github link, or whatever you are using for your project',
    packages=find_packages()
)
```
After this is done, all a dev will need to do is navigate to the project root directory via a terminal and run `pip install -e .`, which will use pip to download the package to their local env and allow for absolute imports in their source code.

### Create intial `environment.yml` or `requirements.txt` file
One difficulty of working on a project with many people is getting everyone on the same page as regards project dependencies. The natural solution is to use a virtual environment and upload a `requirements.txt` or `environment.yml` file to github. For DS projects, I recommend using conda environments, as their dependency management is miles above the competition, though my experience is admittedly limited on some of the other options like `poetry`. 

In addition to this, there are some libraries that are so ubiquitous in Data Science projects that I recommend seeding the `environment.yml` file with some of these top libraries so that everyone starts on the same page. These packages include numpy, pandas, sklearn, and jupyter, as well as linting, testing, and misc libraries such as mypy, flake8, pytest, nbstripout, pre-commit, etc. Depending on the project, XGBoost and fbprophet may also fit the bill.

 (NOTE: If your project involves time series and you plan on using fbprophet, it currently does not support python 3.8 as of the time of this writing, so make sure to either include `fbprophet` in your list of seeded libraries, or specify python=3.7 when you create your conda env.)

So my recommendation is to run the following commands in the project root directory:
1. `conda create -n <shorthand-project-name-for-env> numpy pandas scikit-learn jupyter jupyter_contrib_nbextensions mypy flake8 pytest pytest-cov nbstripout pre-commit`
2. `conda env export --no-builds | grep -v "prefix" > environment.yml`

The second command will export the environment with version numbers (but not build identifiers) to a file called `environment.yml` which devs can then use by navigating to the project root directory and running `conda env update && conda activate <shorthand-project-name-for-env>`. This will ensure that all devs are using conda, virtual environments, and everyone is using the same versions of the most important packages. As the project evolves and dependencies grow, you may need to consolidate various envs, but this gets all devs started off on the same page.

### Create `.pre-commit-hooks.yaml` file
For the uninitiated, git provides a miniature version of Continuous Integration (CI) via git hooks. I recommend looking these up, but essentially you can instruct git to run certain code at various stages of the git workflow, noteably `pre-commit`. What this means is you can force certain linting standards to be met before devs can commit their code and consequently push upstream to their branches. Everyone is going to have a different opinion about this, but I think the following checks are highly beneficial to include as pre-commit hooks

- nbstripout: This program ensures that all output has been stripped from notebooks which is very beneficial for VC
- mypy: I am firmly of the belief providing type hints in python makes for better code, so I recommend enforcing their use
- flake8: Helps adhere to PEP8 standards. Feel free to add in any ignores that better suit your company's style guide

Here is an example `.pre-commit-hooks.yaml` file that I use for all of my projects (note that you will need to edit one of the mypy entries):

```yaml
repos:
- repo: https://github.com/pre-commit/pre-commit-hooks
  rev: v2.4.0
  hooks:
    - id: check-yaml
    - id: end-of-file-fixer
    - id: trailing-whitespace
- repo: https://gitlab.com/pycqa/flake8
  rev: 3.7.8
  hooks:
    - id: flake8
      types: [file, python]
      args: ['--ignore=E401', '--max-line-length=160']
- repo: https://github.com/pre-commit/mirrors-mypy
  rev: v0.780
  hooks:
    - id: mypy
      args: [--ignore-missing-imports, --disallow-untyped-defs]
      files: notebooks/
    - id: mypy
      args: [--ignore-missing-imports, --disallow-untyped-defs]
      files: <pkg_name>  <--- NOTE: CHANGE THIS TO YOUR PROJECT'S NAME AS SPECIFIED IN THE PROJECT ROOT DIRECTORY
- repo: https://github.com/kynan/nbstripout
  rev: master
  hooks:
    - id: nbstripout
      files: ".ipynb"
```

One thing I will note here is that I do not include pytest in my pre-commit hooks. This is because testing can take a lot of time and can consequently discourage devs from commiting often (as they should be doing). However, pytest is included in the CI pipeline, which is discussed later in the article. However, speaking of testing...

### Create `tests/` directory
Code should be tested, and DS code is no different. I very rarely see this discussed, further evidenced by the fact that there is no tests directory in the cookiecutter project template which baffles me. If we are scientists, what is more important than ensuring accurate code and reproducibility? Tests help us do this, and instantiating a culture of testing in your team will make life a lot easier in the long run. In data science there are a lot of assumptions that are made, such as "I don't expect there to be nans in this column" or "this is a cumulative column, so it should be monotonically increasing". However, these assumptions do not always hold up over time (especially if another team manages the underlying data) and code / models can very easily break if underlying assumptions are broken. Therefore we should all be baking tests into our workflows and ensuring our assumptions stay valid and our code covers edge cases where appropriate.

For testing in python I recommend using pytest. If you're not already familiar, there are endless resources online. I can recommend the following video: [link](https://www.youtube.com/watch?v=4fUzlBbLOaw). You can also incorporate propert-based testing using the [`hypothesis`](https://hypothesis.readthedocs.io/en/latest/) library to generate tests which the linked video also covers.

I recommend setting a certain threshhold for code coverage to in order to ensure that testing is in fact being done, though code coverage is a notoriously a bad metric to determine the quality of your tests. Percentage coverage is up to you, but I would recommend 70-80%. This can be enforced via CI which we come to presently.

### Set up CI
Figure out what service your company uses for continuous integration and make the appropriate file for integrating CI into your project. For instance, IBM uses TravisCI, so I use the following file in for my CI pipeline:

```yaml
language: python
python:
  - "3.6"
install:
  - sudo apt update
  # We do this conditionally because it saves us some downloading if the
  # version is the same.
  - wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh;
  - bash miniconda.sh -b -p $HOME/miniconda
  - source "$HOME/miniconda/etc/profile.d/conda.sh"
  - hash -r
  - conda config --set always_yes yes --set changeps1 no
  - conda config --prepend channels conda-forge
  - conda update -q conda
  # Useful for debugging any issues with conda
  - conda info -a

  - conda env update
  - conda activate sf_cri
  - python setup.py install
script:
  - python -m pytest --cov=<pkg_name> --cov-fail-under=80
  - mypy --ignore-missing-imports --disallow-untyped-defs
  - flake8 --ignore=E401 --max-line-length=160
```

The mypy and flake8 checks will already be handled by the pre-commit git hooks we mentioned earlier, but this will ensure that the devs adhered to the reqs. NOTE: You will need to change the `--cov=` value. Additionally, change the `--cov-fail-under` value to your intended coverage percentage.

### Set up Data Infrastructure
The next thing on your list of to-do's should be to figure out what your data infrastructure is going to be. This _could_ be flat files in the data directory of the project, but I really don't recommend this as a longterm solution. Databases are your friend and you should use them. Whether it is on-prem or cloud-based is not of consequence, I would just recommend that you set up the database using whatever tools you are familiar with. I can recommend using SQLAlchemy to build the tables and structure in python. Feel free to start with a simple db like SQLite, but you may want to migrate to a more robust db like postgres once you have worked out the SQLAlchemy scripts. That said, I think SQLite is a perfectly suitable DB for small projects and there isn't much of an argument to be made for switching unless you anticipate the project needing to scale massively in the future.

### Write "Getting Started" section of README file
Make it as easy as possible for your devs to get up and running now that you have implemented the above structures. An example "Getting Started" section may look like the below:

```
### Getting Started
This project assumes you have Anaconda or Miniconda installed on your machine. If you do not, please install from https://docs.conda.io/en/latest/miniconda.html

1. `git clone` this repo in the desired directory on your local machine
2. `cd` into the project directory
3. Run `conda env update && conda activate <pkg_name>`
4. Run `pip install -e .`
5. Run `pre-commit install`
```

Note: If you plan on using Sphinx for documentation automation, then make sure your READMEs are in RST instead of the more traditional markdown.

## Room for improvement
There's lots. I'm still fleshing out some of these files and processes, but some immediate room for improvement is the following:
- Separate test-environment.yaml file that does not install jupyter and its dependencies. This is a very heavy package and makes CI take even longer than it already does.
- Notes around documentation automation via sphinx or pdoc
- Notes around project management via github issues & github projects (trello, jira, etc. as alternatives)

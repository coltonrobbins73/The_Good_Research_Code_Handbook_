+++
title = 'Setting Up Your Project'
date = 2024-04-11T20:26:33-07:00
draft = false
weight = 3
+++

To start a new project :

1. Make a new local folder.
2. Initialize a git repository locally and remotely. Connect the local and remote repositories.
3. Set up a virtual environment preferably with VScode as in [this tutorial](https://code.visualstudio.com/docs/python/environments).

### Making a project skeleton

Consistent directory structures from project to project save time. Python is typically less standardized than other languages but this is a good starting template for your directory :

1. `data` : raw project data that typically is included in `.gitignore` unless data is exceptionally small.
2. `docs` : documentation Markdown files. Calling it `docs` makes it easy to publish documentation with Github pages.
3. `results` : processed data including checkpoints, hdf5, and figures/tables. This would go under `.gitignore` if it becomes too heavy.
4. `scripts` : all execution files including python, bash, and notebooks.
5. `src` : reusable python modules for your project that you would import.
6. `tests` : tests for your code.

**Quickly make this structure with the following command :**

    mkdir {data,docs,results,scripts,src,tests}

7. **Files**
    - `.gitignore` : contains path patterns for files that shouldn't be sourced to version control.
    - `README.md` : project information that gets posted to your repository home page.
    - `environment.yml` : contains details on your environment packages.

**Command to make these files**

    touch {.gitignore,README.md}

### Install a project package

Pathing your different modules so your scripts run properly can be accomplished in one of two ways :

###### 1. Change python path (BAD)

Put the `src` folder on your python path or append dynamically

    import sys
    sys.path.append('/home/me/Documents/codebook/src')

    from src.lib import my_very_good_function

This method is brittle due to hard coding directory names which will break on other systems that want to use your code.

###### 2. Create a pip-installable package (GOOD)

Create a `setup.py` file in the root of your project (just paste this into the terminal):

    cat >> setup.py << EOF
    from setuptools import find_packages, setup

    setup(
    name='src',
    packages=find_packages(),
    )
    EOF

Create an empty `__init__.py` file in the `src` directory which allows the `find_packages` function to find the package.

    touch src/__init__.py

Directory structure so far :

    | -- data
    | -- doc
    | -- results
    | -- scripts
    | -- src
    | -- __init__.py
    | -- tests
    -- .gitignore
    -- environment.yml
    -- README.md
    -- setup.py

Install your package.

    pip install -e .

The `.` indicates that the package is installed in the current directory. The `-e` flag means that the package is editable so if you change files in `src`, the package will update immediately.

Now that the package is locally installed, you can access scripts from it regardless of which directory you are in. When you install a package in editable mode, python automatically adds the package code to its path.

Note that you can change the name of the package. The default is the parent directory `src` so to change the package name, just rename the folder.

If you want to skip all this, you can use cookiecutter to automate all these steps.

Install cookiecutter

    python3 -m pip install --user cookiecutter

Run the specific template for this project

    cookiecutter gh:patrickmineault/true-neutral-cookiecutter

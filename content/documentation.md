+++
title = 'Documentation'
date = 2024-04-12T13:15:19-07:00
draft = false
weight = 7
+++

Documentation refers to all metadata that helps to explain the functions of your code. This includes:

- **Inline comments**
- **Docstring comments**
- **README files**
- **Notebook tutorials**
- **Make files**
- **Unit tests** (demonstrate the intended function behavior)

This information is for others but it is mostly for your future self.

### Error messages over documentation

Practically speaking, people will likely not read the docs for your program so it is usually better to force them to use your program correctly. Impose strict assertions for each functions with corresponding error messages to explicitly tell the user what went wrong and how to fix it.

### Correct code over comments

Before writing any comments, ask yourself if you can rewrite this code so that the comment is not necessary. The best code is one that explains itself through intuitive simple design.

- **Variable naming**
- **Code architecture**

### Publish docs on Readthedocs

Function docstrings can be automatically parsed from your library into a Readthedocs page. Try using Sphinx to quickly accomplish this.

    pip install sphinx
    cd docs
    sphinx -quickstart
    make html

### Write console programs and record overall workflow

Comparing variations of your analysis pipeline should not rely on commenting/uncommenting source code. Instead, it is better to use arguments with something like `argparse` which can route your pipeline based on your initial command line flags.

Once you have settled on a pipeline variant you like, you should construct a shell file or make file to document the workflow steps and arguments that you selected.

### Use hash records for all generated content

If you create any figure or data output. It is a good idea to store the git hash number along with that file name to perfectly encapsulate the program state that generated that figure. If you need to retrieve that specific figure version, you can simply revert to that git commit hash.

    import git
    import matplotlib.pyplot as plt

    repo = git.Repo(search_parent_directories=True)
    short_hash = repo.head.object.hexsha[:10]

    # Plotting code goes here...
    plt.savefig(f'figure.{short_hash}.png')

### Craft a good README.md file

Analogous to a paper abstract, README files show the reader the worth of your project. Here is a good skeleton for a README.md:

1. One sentence description
2. More detailed description
3. Installation
4. General orientation to codebase and instructions
5. Links to papers
6. Links to docs
7. License

+++
title = 'Notebook Organization Tips'
date = 2024-04-12T11:51:03-07:00
draft = false
weight = 4
+++

### Notebooks are not for development

Software development is best contained within scripts and modules. Operations like input/output, ML training pipelines, and functions should be omitted from jupyter notebooks. Reserve notebooks for strict data analysis and visualization and take some time to outline exactly what will be achieved with each notebook beforehand to prevent bloat.

### Top to bottom fast notebook workflow

Ensure that notebooks can run without error from top to bottom. Use restart and run all before finalizing a notebook.

Notebooks are for analysis documentation and presentation only. Move all heavy-lifting functions to separate modules or scripts that should be called through command line or workflow management software.

### Updating modules in notebooks

Automatically update a module within a notebook using:

    %load_ext autoreload
    %autoreload 2

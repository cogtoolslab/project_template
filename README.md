# Project Template

This is an example of how a cogtoolslab project repo should be organized.

It contains several subdirectories that will contain standard elements of almost every project:

- `analysis` (aka `notebooks`): This directory will typically contain jupyter/Rmd notebooks for exploratory code development and data analysis.
- `experiments`: If this is a project that will involve collecting human behavioral data, this is where you want to put your experimental code. If this is a project that will involve evaluation of a computational model's behavior on a task, this is also where you want to put the task code.
- `model`: If this is a cognitive modeling project, this is where you want to put your model definitions. If this project involves training neural networks, you might consider starting out putting training scripts in here, but then splitting these off into a separate `training` dir. 
- `results`: This directory is meant to contain "intermediate" results of your computational/behavioral experiments. It should minimally contain two subdirectories: `csv` and `plots`. So `/results/csv/` is the path to use when saving out `csv` files containing tidy dataframes. And `/results/plots/` is the path to use when saving out `.pdf`/`.png` plots, a small number of which may be then polished and formatted for figures in a publication. *Important: Before pushing any csv files containing human behavioral data to a public code repository, triple check that this data is properly anonymized. This means no bare AMT Worker ID's.*
- `stimuli`: This directory is meant to contain any download/preprocessing scripts for data that are _inputs_ to this project. For many projects, these will be images. This is also where you want to place any scripts that will upload your data to our `stimuli`  MongoDB database and any image data to Amazon S3 (so that it has a semi-permanent URL you can use to insert into your web experiment.)
- `utils`: This directory is meant to contain any files containing helper functions. 

### Note about storing code vs. data on GitHub
A good rule of thumb is to think of GitHub as a tool to store _code_ and _not data_. There are some exceptions to this rule, e.g., when we want to make it easier for others to download our tidy experimental dataframes as `.csv` files and re-analyze them. But these files should not be too large. >100MB is too large, and >10MB is a little bit too large. If you need a place to store a large public dataset, there are other resources we can use besides GitHub. If you simply need to share a dataset with a colleague/collaborator within cogtoolslab or at UCSD, there is likely to be another option (e.g., on a shared filesystem we all have access to).

So one of the first things to do is to update the `.gitignore` in your new project repo. Add these lines to ignore common data files (e.g., images, videos, byproducts of compiling LaTeX source, etc.) and anything likely to contain sensitive information (e.g., auth text files). Also ignore the annoying `.DS_Store` file that is part of MacOS. 

```
.DS_Store
*.csv
*.json
*.pdf
*.png
*.jpeg
*.jpg
*.tiff
*.svg
*.eps
*.ai
auth.json
auth.txt
```

### GitHub Hygiene Basics

Here are some basic GitHub hygiene practices we encourage:

0. When you sit down to start working, it is good practice to run `git pull` to pull in any changes that have been made to the repo since you last finished working. This will help to reduce the chance of nasty merge conflicts by making sure that you've synchronized your clone with the remote repo before starting to make new changes. 

1. It is generally better to make several small commits than one large, complex commit. In many cases, this means running `git add` on just a single file at a time! This allows you to leave more informative commit messages for your collaborators (including your future self).

2. Before you push, use `git diff` to inspect changes before committing to make sure they are what were intended. To get out of the git diff view, press `q`.

3. Fixing merge conflicts can be a pain. Basically, when you run into a merge conflict, inhale+exhale, then open up the file in question to identify which version of the code to keep and which to discard. You need to do this manually. Any file that still has this motif in it `<<<<<<< HEAD` anywhere at all in the file still has a merge conflict, and won’t execute. Various fancier text editors, e.g., Atom, have ways of easing this process, but you still want to be vigilant to make sure that these fancy editors are parsing the conflicting region properly.

4. Use `git mv` and `git rm` to "rename" files when moving them around, rather than the bare `mv` and `rm`, b/c this will make sure that the git history moves around with these files and they are not removed from the history. 

5. Generally speaking, you want to "restart and clear all output" from your jupyter notebooks before you commit them. This will keep the file size down and make it easier for collaborators to open and run them.

### Note about other project documentation 

#### Starter Google Doc

When we spin up a new project, the first thing we'll often do to collect our thoughts is create a Google Doc. This is b/c this file format is easy to share and flexible in format. This google doc is also where you should take notes during our meetings, and collect high-level TODO items, especially those that are not immediately actionable in code. .For code development TODO's, we will often instead use GitHub Issues.

#### Open Science Framework for pre-registration of behavioral experiments

Once we are in the later stages of desigining a new human behavioral experiment and preparing to run our first pilot, we will write up a pre-registration and post it to the [Open Science Framework](https://osf.io/). We subscribe to the philosophy that "pre-registrations are a plan, not a prison." They help us transparently document our thinking and decision-making process both for ourselves and for others, and will help us distinguish between confirmatory and exploratory findings. We do not believe that there is a single best way to write a pre-registration, but in many cases a more detailed plan will help us to clarify our experimental logic and set up our analyses accordingly (i.e., what each hypothesis predicts, which measures and analyses we will use to evaluate each relevant hypothesis). 

#### Manuscripts (including conference papers/abstracts) 

When we are preparing to write up a manuscript (or a conference paper), we will create a new repo, usually following the convention: `projectname_latex`. This is where you will want to place your LaTeX source `.tex` files for your paper and your publication-ready figures as high-resolution `.pdf` files in the `figures` directory. We typically format and fine-tune our figures using Adobe Illustrator.

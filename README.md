# course-template repo

This repository is a template for courses and webpages for self-learning.

## Using this template

### Click the green `Use this template` button to the top right.
  
In the pop-up window:

   1. Choose an organisation where the repository will be hosted
   2. Enter a name for the new repository (keep in mind that this will be part of the URL)
   3. Decide if the repository should be Public (most likely) or Private
   4. Make sure to tick `Include all branches`
   5. Click **`Create repository from template`**

![](./tmp/new_repo_from_template.png)

### Add collaborators
Go to settings and select `Collaborators and teams` under `Access` in the left side menu 

1. Click one of the green buttons `add people`  or `add teams`
2. Select a person or a team to invite
3. Selet the appropriate role 
4. Click `add user to this repository`

![](./tmp/add_collaborators.png)

### Update the README.md
Modify and add information about the new workshop/course.

### Delete the tmp folder
The tmp folder just supports this README file, so you can just delete it after modifying it.

## The branches

### main branch

The main branch is a folder template to create the actual materials for a workshop session. Notebooks, exercises and materials associated to them (like images) should be here. 
On the other hand, actual data and slides are too big for a github repository. Such materials should be hosted in a [zenodo](https://zenodo.org/) repository.

#### Hosting data and slides in Zenodo

Zenodo is a Open Science data repository from the OpenAIRE project supported by [CERN](https://home.cern/) to ensure that everyone can join in Open Science. 
It allows researchers to upload many different types of data and gives each repository a unique and citeable identifier (DOI). 
We can also link a Github repository and whenever you create a release for the github repo, it will give it as well a DOI. 
Follow this [link](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content) for instructions 
We are using Zenodo to deposit slides, materials and data necessary for the course, relieving the size of the Github repo. It also makes it easier to update the materials and use them in the UCloud apps.

### webpage-mkdocs branch

The webpag-mkdocs branch contains all the content needed to create and deploy the self-learning part of the course/workshop. 
For more instructions, including how to set up Github Pages and automatic deploying of the webpage, check the README.md file from the [webpage branch](https://github.com/hds-sandbox/course-template/tree/webpage).
Note: MkDocs requires a lot of plugins, which can be deprecated over time. You can use the branch `webpage-quarto` which does not require extra packages and will be more longeve.

### webpage-quarto branch

The webpag-quarto branch contains - as above - an example of webpage to create and deploy the self-learning part of the course/workshop. Go to the branch to see what you need (`quarto` and few `R` packages) to get going.

### gh-deploy branch

The tool that you can use to create a course website is wither [`mkdocs`](https://www.mkdocs.org/) or [`quarto`](https://quarto.org/), depending on which you prefere from the two github branches above.
Mkdocs has a specific command `mkdocs gh-deploy` that takes the content of a branch and creates and deploys the website in a new branch called "gh-pages". The same for `quarto deploy gh-pages`.
Here, one of the branches "webpage-mkdocs" and "webpage-quarto" can be used to create the website. Once you save the changes pushing them to github, a github workflow will automatically deploy the website using an appropriate github action.
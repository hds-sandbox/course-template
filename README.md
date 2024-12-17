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
3. Select the appropriate role 
4. Click `add user to this repository`

![](./tmp/add_collaborators.png)

### Update the README.md
Modify and add information about the new workshop/course.

### Delete the tmp folder
The tmp folder just supports this README file, so you can delete it after modifying it.

## The branches

### main branch

The main branch is a folder template to create the actual materials for a workshop session. Notebooks, exercises and materials associated to them (like images) should be here. **Maintaining only one version of the coding material is essential to ensure consistency and avoid confusion. Please do not make copies on the server or locally; use version control for edits instead.**

On the other hand, actual data and slides are too big for a GitHub repository. Read the next section about hosting data in a [zenodo](https://zenodo.org/) repository. Consider what is the best strategy for hosting or sharing slides. For collaborative questions, there is a copy in SharePoint.

#### Hosting data in Zenodo

Zenodo is an Open Science data repository from the OpenAIRE project supported by [CERN](https://home.cern/) to ensure that everyone can join in Open Science. 
It allows researchers to upload many different types of data and gives each repository a unique and citeable identifier (DOI). 
We can also link a GitHub repository and whenever you create a release for the GitHub repo, it will give it as well a DOI. 
Follow this [link](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content) for instructions 
We are using Zenodo to deposit complementary materials and data necessary for the course, relieving the size of the GitHub repo. It also makes it easier to update the materials and use them in the UCloud apps.

### webpage-mkdocs branch (older solution)

The webpage-mkdocs branch contains all the content needed to create and deploy the self-learning part of the course/workshop. 
For more instructions, including how to set up GitHub Pages and automatic deploying of the webpage, check the README.md file from the [webpage branch](https://github.com/hds-sandbox/course-template/tree/webpage-mkdocs).
Note: MkDocs requires a lot of plugins, which can be deprecated over time. You can use the branch `webpage-quarto` which does not require extra packages and will be more longeve.

### webpage-quarto branch (recommended)

The webpage-quarto branch contains - as above - an example of a webpage to create and deploy the self-learning part of the course/workshop. Go to the branch to see what you need (`quarto` and a few `R` packages) to get going.

### gh-pages branch

The tool that we use to create the website is called [`mkdocs`](https://www.mkdocs.org/) with the theme [`material`](https://squidfunk.github.io/).
Mkdocs has a specific command `mkdocs gh-deploy` that takes the content of a branch and creates and deploys the website in a new branch called "gh-deploy".
In our case, it would use the branch "webpage" to create our website. 
The branch "webpage" contains a GitHub workflow that will automatically deploy the website using `mkdocs gh-deploy` whenever you push a commit to the webpage branch.

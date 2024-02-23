# Webpage publishing using quarto

This material contains the webpage done with `Quarto`. It contains an automatic deployment script to make it into a live webpage. More in the paragraphs following this introduction.

If you want to produce a webpage on your computer, you only need to install `quarto` and `pandoc`. To use the `R` commands in this webpage example you need optionally the `R` packages `tidyverse, rmarkdown, knitr, gt`. If you are adding `R markdown` files to the webpage, you will need the related packages of their `R` code to make things work.

Following you can read a small guide

## Configuration file

The setup file for your webpage is called `_quarto.yml`. This example has one that contains many commonly used things, but otherwise you can find links to various components to configure your website [here](https://quarto.org/docs/websites/).

### navigation bar

In our configuration, you find the type of `project`, and then the `website` descriptors. Inside the `website`, you have a title and then the configuration for the navigation bar `navbar`. This contains left and right elements:
```yml
    left:
      - href: index.qmd
        text: Introduction
      - href: people.qmd
        text: People
      - href: rmd/rmarkdown_example.Rmd
        text: Rmarkdown      
      - href: jupyter_example.ipynb
        text: Jupyter example
    right: 
      - icon: github
        href: https://github.com/hds-sandbox
        aria-label: GitHub
      - icon: linkedin
        href: https://www.linkedin.com/company/ucph-heads/
        aria-label: LinkedIn
```
On the left there are menu titles and links to other documents used for the subpages. On the right, a couple of icons with social media links. It is very easy to add new pages to the menu on the left to change the structure of the website.

### themes

Following you have html themes for the webpage look both in light and dark mode. Here we use the sandbox colors, and therefore the themes are modified. For the light mode we use the theme `materia`, where some of the elements are modified using a file in `scss` format. The `scss` format is very easy to understand and modifying other elements of the theme is possible with almost no effort (though it should not be needed for a sandbox-style webpage). The dark theme is just a standard one, and we do not pretend to match any sandbox color scheme. 

```yml
format:
  html:
    theme: 
      light: [materia, css/materialight.scss]
      dark: darkly
    toc: true
```

See [this link](https://quarto.org/docs/output-formats/html-themes.html) if you want to see more about modifying a `scss` file with some examples for `Quarto`.

### bioschemas

Finally there is a commented section which includes a bioschema as part of the webpage header. The bioschema is in an html file, whose script is always executed by the deployed webpage. Uncomment this part of the configuration only upon finalization of your website - so that it will be published on the Elixir TeSS database with the proper finish content.

Look into `resources/bioschema.html`, you can see how the bioschema is structured: it is nothing else than a `json` table containing some standard descriptors listing course name, type, audience, datasets and so on.

```json
    {
      "@context": "https://schema.org",
      "@id": "https://hds-sandbox.github.io/",
      "@type": "LearningResource",
      "dct:conformsTo": "https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE",
      "description": "Home page of the danish health data science sandbox",
      "keywords": [
        "# Keyword1, Keyword2, etc"
      ],
      "learningResourceType": [
        "e-learning"
      ],
      "license": [
        {
          "@id": "https://creativecommons.org/licenses/by-sa/4.0/",
          "@type": "CreativeWork"
        }
      ],
      "mentions": [
        {
          "@id": "# Link to DOI or zenodo materials (10.5281/zenodo.7660225)",
          "@type": "Thing"
        },
        {
          "@id": "#Another link to DOI or zenodo materials (10.5281/zenodo.7565997)",
          "@type": "Thing"
        }
      ],
      "name": "# Name of the workshop (Introduction to bulk RNAseq analysis workshop)",
      "educationalLevel": "# One of: Beginner, Intermediate or Advanced",
      "audience": "# PhD, postdocs, MSc, etc"
    }
```

The example above contains the schema standard, `@context`, which is fixed. Then the link to the course, `@id`, and the fact that we are talking about a learning resource, `@type`. Then you find some keywords, the type of learning resource, a user license. At the `mentions` item you can create multiple objects of `@type: Thing` with a link (`@id`). Those can be datasets, slides, and other open material. Finally you have a few other descriptors for the course. If you want to see a more complete example, look at the file `resources/bioschema_example.html` to get inspiration. Look at the  [bioschemas for training material](https://bioschemas.org/profiles/TrainingMaterial/1.0-RELEASE) for exploring all terms that can be used in a bioschema. You can copy your bioschema or the webpage address (once is published with the bioschema included in the configuration file) [here](https://validator.schema.org/) to verify it: simply put your code from `bioschema.html` or the published webpage to get a report on the elements of the bioschema.

## Writing a webpage in `qmd` format

A standard webpage is in `qmd` format. This is nothing else than a markdown document with some metadata at the very beginning, explaining a few things (references, which date to show, and few other things). You can also use a admonitions and pieces of code, which you can execute. The webpage `index.qmd` is a basic example that contains some elements.

## Adding Rmd files

`R markdown`, or `Rmd`, files can be used as webpages (see one of the menu items in the configuration file). Those need to be knitted and executed, so you need all the relevant R packages to do so. Other than that, the `Rmd` file will become a nice looking webpage, where you can also include bibliography. Look at the example page `rmd/rmarkdown_example.Rmd` to see how things need to be coded.

## Adding jupyter notebooks

Files in `ipynb` can similarly be used as webpages, but you do not need to compile them when you create the webpage. They will just be read in as they are and converted into a webpage. Interactive plots, if present, should be working also in web format.

## Listing people

You can create pages containing lists (as for example listing blog items or other lists). You can see how the page `people.qmd` has a specific metadata dedicated to this:

```yml
---
title: "People"
listing:
  contents: cards/*.qmd
  type: default
---
```

The webpage wants to show the people in the sandbox project. Those are all in the folder `cards` - there is a `qmd` file per person, with a picture and description and some links. We tell the listing where to find the items to show using the option `content`.

## Push 'n Publish

If you want to see the webpage under development, you can simply run the comman `quarto preview` from your command line, while inside the folder with the configuration file.

The webpage can be published by simply pushing it on github. There is a github workflow in the folder `.github\workflows\publish.yml` which does all of that. Unfortunately, if you need additional `R` packages, then you need to change the workflow on your own. You can do this by taking a `snapshot` from the R you use for development (after loading all needed packages). That should produce a file called `renv.lock` you can use to substitute the one present in this repository.

It can be very annoying trying to make the workflow work and testing it until it does. You can also deploy manually the webpage by 

* deleting the workflow file `.github\workflows\publish.yml` which will otherwise always try to run
* run `quarto publish gh-pages` on your command line
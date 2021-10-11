# MindsDB Documentation
[![Build Status](https://travis-ci.org/mindsdb/mindsdb-docs.svg?branch=master)](https://travis-ci.com/mindsdb/mindsdb-docs)
   <a href="https://community.mindsdb.com/"><img src="https://img.shields.io/discourse/posts?server=https%3A%2F%2Fcommunity.mindsdb.com%2F" alt="MindsDB Community"></a>
  <img alt="Website" src="https://img.shields.io/website?down_color=red&down_message=offline&up_color=green&up_message=online&url=https%3A%2F%2Fdocs.mindsdb.com%2F">
  
  
![](https://res.cloudinary.com/crunchbase-production/image/upload/c_lpad,h_170,w_170,f_auto,b_white,q_auto:eco,dpr_1/tkxsf7gdmc752a1wng8u)
## Running the docs locally

First, install the mkdocs and mkdocs-material theme in your python virtual environment:
```
pip install -r requirements.txt
```
Then, navigate to the `/mindsdb-docs` directory and start the server:

```
mkdocs serve
```

The documentation website will be available at `http://127.0.0.1:8000`

![](https://mindsdb.com/wp-content/uploads/2021/09/hero-img-new.svg)

## Deploy the docs

The latest version shall be automatically pushed and deployed after merge on master. If the CI/CD deploy failed, locally run:

```
mkdocs gh-deploy
```

All of the HTML files and assets will be pushed to the [gh-pages](https://github.com/mindsdb/mindsdb-docs/tree/gh-pages) branch and published on github pages.

## Repository structure

The mindsdb-docs layout is as follows:

```
docs                                   # Containes documentation source files
|__assets/                             # Image and icons used in pages
|__.md                                 # All of the markdown files used as pages
overrides
├─ assets/
│  ├─ images/                          # Images and icons
│  ├─ javascripts/                     # JavaScript
│  └─ stylesheets/                     # Stylesheets
├─ partials/
│  ├─ footer.html                      # Footer bar
├─ 404.html                            # 404 error page
├─ base.html                           # Base template
└─ main.html
.mkdocs.yml                            # Mkdocs configuration file
```
# Contribute

## How can you help us? [![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/mindsdb/mindsdb-docs/issues)

* Report a bug
* Improve documentation
* Propose new feature
* Fix typos

## Contributors

<a href="https://github.com/mindsdb/mindsdb-docs/graphs/contributors">
  <img src="https://contributors-img.web.app/image?repo=mindsdb/mindsdb-docs" />
</a>

Made with [contributors-img](https://contributors-img.web.app).

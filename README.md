# MindsDB Documentation


## Running the docs locally

First install the mkdocs in your python virtual environment:
```
pip install mkdocs
```
Then, navigate to the `/mindsdb-docs` directory and start the server:

```
mkdocs serve
```

The documentation website will be avaiable at `http://127.0.0.1:8000`


## Deploy the docs

The latest version shall be automaticly pushed and deployed after merge on master. If the CI/CD deploy failed, locally run:

```
mkdocs gh-deploy
```

All of the html files and assets will be pushed to the [gh-pages](https://github.com/mindsdb/mindsdb-docs/tree/gh-pages) branch and published on github pages.

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
## How can you help us?
* Report a bug
* Improve documentation
* Propose new feature
* Fix typos


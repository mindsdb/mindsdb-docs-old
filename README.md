# MindsDB Documentations 


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

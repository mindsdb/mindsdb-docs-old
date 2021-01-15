# Install MindsDB froum source

This section describes how to install MindsDB from source. This is a prefered way to install MindsDB in case you want to contribute to our code or simply debug the MindsDB.

## Prerequisite

* [Python version](https://www.python.org/downloads/) >=3.6 (64 bit) and pip version >= 19.3.
* [Pip](https://pip.pypa.io/en/stable/installing/) (usually is pre installed with latest Python versions).
* [Git](https://git-scm.com/).

## Installation

We recommend to install MindsDB inside virtual environment to avoid dependency issues.

1. Clone the repository:

    ```
    git clone git@github.com:mindsdb/mindsdb.git
    ```

2. Create virtual environment and activate it:

    ```
    python3 -m venv mindsdb
    source mindsdb/bin/activate
    ```

3. Install requirements:

    ```
    cd mindsdb && pip install -r requirements.txt
    ```

4. Install MindsDB:

    ```
    python setup.py develop
    ```

5. You're done!

To check if everything works, start MindsDB server:

```
python -m mindsdb
```

* To access MindsDB APIs visit `http://127.0.0.1:47334/api`.
* To access MindsDB Scout visit  `http://127.0.0.1:47334/`


## Install troubleshooting

!!! failure "No module named mindsdb"
    If you got this error, make sure that your virtual environment is activated.

!!! failure "ImportError: No module named {dependency name}"
    In case you skipped the 3th step, simmilar error can happen. Make sure that you install all of the MindsDB requirements.

!!! failure "This site can’t be reached. 127.0.0.1 refused to connect."
    Please check the MindsDB server console in case the server is still in `starting` phase. If server started and there is some error displayed, please
    report that on our [GitHub](https://github.com/mindsdb/mindsdb/issues).
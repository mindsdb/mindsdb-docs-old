
## Install using MindsDB installers

Install MindsDB on your MacOS machine using an easy-to-use shell script.

!!! tip "Download the script"
    [MindsDB for MacOS](https://mindsdb-installer.s3-us-west-2.amazonaws.com/mindsdb-installer/osx/MindsDB_Server_v1.4.1.dmg)

This script will install MindsDB and MindsDB's dependencies, and start the MindsDB server.
> Note that you need Python 3.6.x, 3.7.x or 3.8.x pre installed.

## Install using Anaconda

You will need [Anaconda](https://www.anaconda.com/products/individual) or [Conda](https://conda.io/projects/conda/en/latest/index.html) installed and Python 64bit version. Then open Anaconda Prompt and:

1. Create new virtual environment and install mindsdb:

    ```
    conda create -n mindsdb
    ```

    ```
    conda activate mindsdb
    ```

    ```
    pip install mindsdb
    ```

2. To verify that mindsdb was installed run:

    ```
    conda list
    ```

You should see a list with the names of installed packages.

### Install using pip

We suggest you to install MindsDB in a virtual environment when using **pip** to avoid dependency issues. Make sure your Python version is **>=3.6** and pip version **>= 19.3**.

1. Create and activate venv:

    ```
    python -m venv mindsdb
    ```

    ```
    source mindsdb/bin/activate
    ```

2. Install MindsDB:

    ```
    pip install mindsdb
    ```

3. To verify that mindsdb was installed run:

    ```
    pip freeze
    ```

You should see a list with the names of installed packages.

!!! failure "Installation fail"
    Don't worry, simply follow the below bellow instruction which should fix most issues.


1. If you got `numpy.distutils.system_info.NotFoundError: No lapack/blas resources found. Note: Accelerate is no longer supported.` error when installing on macOS and you are using **Python 3.9** please, downgrade to older versions for now. We are working on this and **Python 3.9** will be supported soon.

2. **Python 64** bit version is required. 

3. If you are using macOS and got error about system dependencies, try installing MindsDB with [Anaconda](https://www.anaconda.com/products/individual) and run the installation from the **anaconda prompt**.

4. If none of this works, try installing mindsdb using the [docker container]() and create an issue with the installation errors you got on our  [Github repository](https://github.com/mindsdb/mindsdb/issues) and we'll try to review it within a few hours.
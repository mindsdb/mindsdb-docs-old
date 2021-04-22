
## Install using MindsDB installers

Install MindsDB on your MacOS machine using an easy-to-use shell script.

!!! tip "Download the script"
    [MindsDB for MacOS](https://mindsdb-installer.s3-us-west-2.amazonaws.com/mindsdb-installer/v2/osx/MindsDBInstaller_1.5.dmg)

This installer will install Python3, MindsDB and MindsDB's dependencies.

## Install using Anaconda

!!! warning "Python 3.9"
    Currently, some of our dependencies have issues with the latest versions of Python 3.9.x. For now, our suggestion is to use Python 3.6.x, 3.7.x, or 3.8.x versions.

You will need <a href="https://www.anaconda.com/products/individual" target="_blank">Anaconda</a> or <a href="https://conda.io/projects/conda/en/latest/index.html" target="_blank">Conda</a> installed and a Python 64bit version. Then open the Anaconda prompt and:

1. Create a new virtual environment and install mindsdb:

    ```
    conda create -n mindsdb
    ```

    ```
    conda activate mindsdb
    ```

    ```
    pip install mindsdb
    ```

2. To verify that mindsdb was installed, run:

    ```
    conda list
    ```

You should see a list with the names of installed packages.

### Install using pip

!!! warning "Python 3.9"
    Currently, some of our dependencies have issues with the latest versions of Python 3.9.x. For now, our suggestion is to use Python 3.6.x, 3.7.x, or 3.8.x versions.
    
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

3. To verify that mindsdb was installed, run:

    ```
    pip freeze
    ```

You should see a list with the names of installed packages.

!!! failure "Installation fail"
    Don't worry; simply follow the instructions below, which should fix most issues.


1. If you got a `numpy.distutils.system_info.NotFoundError: No lapack/blas resources found. Note: Accelerate is no longer supported.` error when installing on macOS and you are using **Python 3.9**, please downgrade to an older version of Python for now. We are working on this, and **Python 3.9** will be supported soon.

2. **Python 64** bit version is required.

3. If you are using macOS and got an error about system dependencies, try installing MindsDB with [Anaconda](https://www.anaconda.com/products/individual), and run the installation from the **anaconda prompt**.

4. If none of this works, try installing mindsdb using the [docker container](/installation/docker), and create an issue with the installation errors you got on our [Github repository](https://github.com/mindsdb/mindsdb/issues) and we'll try to review it within a few hours.


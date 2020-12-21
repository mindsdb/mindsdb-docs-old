
## Install using MindsDB installers

Install MindsDB on your Linux machine using an easy-to-use shell script.

!!! tip "Download the script"
    [MindsDB for Linux](https://mindsdb-installer.s3-us-west-2.amazonaws.com/mindsdb-installer/v2/linux/MindsDBInstallerBeta_1.5.sh)

This script will install MindsDB and MindsDB's dependencies, and start the MindsDB server.
> Note that you need Python 3.6.x, 3.7.x or 3.8.x installed.

## Install using pip

We suggest you to install MindsDB in a virtual environment when using **pip** to avoid dependency issues. Make sure your Python version is **>=3.6**.

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


!!! failure "Installation fail"
    Don't worry, simply follow the below bellow instruction which should fix most issues.


1. **Python 64** bit version is required. 

2. If you are using **Python 3.9** you may get installation errors. Some of the MindsDB's dependencies are not working with **Python 3.9**, so please downgrade to older versions for now. We are working on this and **Python 3.9** will be supported soon.


3. If you are using Linux install `tkinter` from your package manager in certain situations.
    - Ubuntu/Debian: `sudo apt-get install python3-tk tk`
    - Fedora: `sudo dnf -y install python3-tkinter`
    - Arch: `sudo pacman -S tk`

4. If none of this works, try installing mindsdb using the [docker container]() and create an issue with the installation errors you got on our  [Github repository](https://github.com/mindsdb/mindsdb/issues) and we'll try to review it within a few hours.
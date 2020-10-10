---
id: installing-mindsdb
title: Installing MindsDB
---

## Prerequisites

Before you begin, you need [**python>=3.7**](https://realpython.com/installing-python/) or [**Conda Python3**](https://www.anaconda.com/download/), and make sure you have the **latest pip3**.

To install python & pip:

```bash
curl https://bootstrap.pypa.io/get-pip.py | python3
pip3 install --upgrade pip
```

To install conda (only required on some windows environments) [download conda from here](https://www.anaconda.com/download/#windows).
Once that's done run the **anaconda prompt**.


Once that's done, you can install mindsdb from your terminal or from the **anaconda prompt**.

## Standard installation

### Install MindsDB with pip:

```bash
pip install mindsdb
```

### Install using virtual environment
We suggest you to run MindsDB on a virtual environment to avoid dependency issues. Make sure your Python version is >=3.6. To set up a virtual environment:

#### Install in Windows
1. Create and activate venv:
```bash
py -m venv venv
.\venv\Scripts\activate
```
2. Install MindsDB:
```bash
pip install mindsdb
```

#### Install in Linux and macOS
1. Create and activate venv:
```bash
python -m venv venv
source venv/bin/activate
```
2. Install MindsDB:
```bash
pip install mindsdb
```
 
### Install using Host Environment
You can use MindsDB on your own computer in under a minute, if you already have a python environment setup, just run the following command:

1. Install MindsDB:
```bash
 pip install mindsdb --user
```

If for some reason this fail, don't worry, simply follow the below [What to do if installation fails](https://docs.mindsdb.com/Installing/#what-to-do-if-installation-fails) which will lead you through a more thorough procedure which should fix most issues.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Uw2Phj5Q0xA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## What to do if installation fails

1. Python 64 bit version is required. Depending on your environment, you might have to use `pip3` instead of `pip`, and `python3.x` instead of `python` in the above commands.

2. Try manually installing pytorch following the simple instructions on their official website: https://pytorch.org/get-started/locally/

3. If you are using Linux install `tkinter` from your package manager in certain situations.
    - Ubuntu/Debian: `sudo apt-get install python3-tk tk`
    - Fedora: `sudo dnf -y install python3-tkinter`
    - Arch: `sudo pacman -S tk`

4. If you are using Windows, but are not using Anaconda or Conda, try installing one of them and running the installation from the **anaconda prompt**.

5. If you've previously installed mindsdb and are having issues upgrading to a new version, try installing with the command: `pip install mindsdb --upgrade`, if that still fails, try: `pip install mindsdb --no-cache-dir --force-reinstall`.

6. If none of this works, try installing mindsdb using the docker container and create an issue with the installation errors you got on: https://github.com/mindsdb/mindsdb/issues, we'll try to review it within a few hours.

<iframe width="560" height="315" src="https://www.youtube.com/embed/SH1nCChpcps" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Build and run your docker container

Alternatively, you can also run MindsDB in a docker container. Assuming that you have [docker](https://docs.docker.com/install/) installed in your computer.
On your terminal, you can do the following:

```
sh -c "$(curl -sSL https://raw.githubusercontent.com/mindsdb/mindsdb/master/distributions/docker/build-docker.sh)"

```

## Hardware

Due to the fact that pytorch only supports certain instruction sets, mindsdb can only use certain types of GPUs.
Currently, on AWS, `g3` and `p3` instance types should be fine, but `p2` and `g2` instances are not supported.
VPS on DigitalOcean with 3 GB Memory and above should work.


## MindsDB Server

After installing MindsDB Server can be started by running:

```
python -m mindsdb
```

You should see simmilar message as:

```
GUI should be available by http://0.0.0.0:47334/static/index.html
Start on 0.0.0.0:47334
Serving on http://0.0.0.0:47334
```

* To access MindsDB API's visit `http://0.0.0.0:47334`.
* To access MindsDB Scout visit  `http://0.0.0.0:47334/static/index.html`
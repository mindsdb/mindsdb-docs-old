

Lightwood is a Pytorch based framework with two objectives:

- Make it so simple that you can build predictive models with a line of code.
- Make it so flexible that you can change and customize everything.

Lightwood was inspired on [Keras](https://keras.io/)+[Ludwig](https://github.com/uber/ludwig) but runs on Pytorch and gives you full control of what you can do.


## Installing Lightwood


### On Linux, OSX, Windows and all other operating systems
```bash
pip3 install lightwood
```

If this fails, please report the bug on github and try installing the current master branch:

```bash
git clone git@github.com:mindsdb/lightwood.git;
cd lightwood;
pip install --no-cache-dir -e .
```

**Please note that, depending on your os and python setup, you might want to use `pip` instead of `pip3`, so please try the commands with `pip` if the ones above fail**

You need python 3.6 or higher.

Note on MacOS, you need to install libomp:

```bash
brew install libomp
```

### Installing Lightwood on Windows

Install `pip` to the latest version

```bash
python -m pip install --upgrade pip
pip --version
```
Install lightwood using `pip`

```bash
pip install lightwood
```
### Installing Lightwood on a Virtual Environment

A virtual environment essentially allows you to create a “virtual” isolated Python installation and install packages into that virtual installation.
`virtualenv` is used to manage Python packages for different projects.
Please ensure to follow these steps for installing lightwood on a virtual environment

#### Installing Virtual Environment

If virtual environment is not installed please do the same by entering the following command for the respective operating system

On macOS and Linux

```bash
python3 -m pip install --user virtualenv
```

On Windows:

```bash
py -m pip install --user virtualenv
```
You can also use `python` instead of `py`

#### Creating the Virtual Environment

After having done the above steps you should create a virtual environment on the respective operating system.

On macOS and Linux:

```bash
python3 -m venv env
```

On Windows:

```bash
py -m venv env
```
You can also use `python` instead of `py`

#### Activating the Virtual Environment

Before installing lightwood in a virtual environment you need to first activate the `venv`

On macOS and Linux:

```bash
source env/bin/activate
```

On Windows:

```bash
.\env\Scripts\activate
```
This will activate the `venv` and now finally lightwood is ready to be installed using `pip`

#### Installing lightwood on `venv`

```bash
pip3 install lightwood
```
This will install lightwood in a virtual environment successfully.
Please keep in mind `pip3` can be replaced with `pip` depending on the os and python setup. 

## Quick example

Assume that you have a training file (sensor_data.csv) such as this one.

| sensor1  | sensor2 | sensor3 |
|----|----|----|
|  1 | -1 | -1 |
| 0  | 1  | 0  |
| -1 | -1 | 1  |
| 1  | 0  | 0  |
| 0  | 1  | 0  |
| -1 | 1  | -1 |
| 0  | 0  | 0  |
| -1 | -1 | 1  |
| 1  | 0  | 0  |

And you would like to learn to predict the values of *sensor3* given the readings in *sensor1* and *sensor2*.

### Learn

You can train a Predictor as follows:

```python
from lightwood import Predictor
import pandas

sensor3_predictor = Predictor(output=['sensor3'])
sensor3_predictor.learn(from_data=pandas.read_csv('sensor_data.csv'))

```

### Predict

You can now be given new readings from *sensor1* and *sensor2* predict what *sensor3* will be.

```python

prediction = sensor3_predictor.predict(when={'sensor1':1, 'sensor2':-1})
print(prediction)
```

Of course, that example was just the tip of the iceberg, please read about the main concepts of lightwood, [the API](API.md) and then jump into examples.

---
id: installing-mindsdb
title: Installing MindsDB
---

There are a few options to install MindsDB on different operating systems. To find the one that works the best for you, check out the below links.

## Installation

=== "Docker"

    !!! info "Installation"
        Follow the [Docker installation](/installation/docker) instructions.

=== "Windows"

    !!! info "Installation"
        Follow the [Windows installation](/installation/Windows) instructions.

=== "Linux"

    !!! info "Installation"
        Follow the [Linux installation](/installation/Linux) instructions.

=== "macOS"

    !!! info "Installation"
        Follow the [macOS installation](/installation/MacOS) instructions.

=== "Source"

    !!! info "Installation"
        Follow the from [source installation](/installation/source) instructions.


## Try out using GoogleCollab

Checkout [![Google Colab](https://colab.research.google.com/assets/colab-badge.svg "MindsDB")](https://colab.research.google.com/drive/1qsIkMeAQFE-MOEANd1c6KMyT44OnycSb) this example on GoogleCollab.


## MindsDB Server

After succesfull installation MindsDB Server can be started by running:

```
python -m mindsdb
```

You should see a similar message to:

```
GUI should be available by http://127.0.0.1:47334/index.html
Start on 127.0.0.1:47334
Serving on http://127.0.0.1:47334
```

* To access MindsDB APIs visit `http://127.0.0.1:47334/api`.
* To access MindsDB Scout visit  `http://127.0.0.1:47334/`

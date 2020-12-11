---
id: installing-mindsdb
title: Installing MindsDB
---

## Installation

=== "Linux"

    !!! info "Installation"
        Follow the [Linux installation](/installation/Linux) instructions.

=== "Windows"

    !!! info "Installation"
        Follow the [Windows installation](/installation/Windows) instructions.

=== "macOS"

    !!! info "Installation"
        Follow the [macOS installation](/installation/MacOS) instructions.

## Install with Docker

If none of the above specific OS installation options doesn't work for you, alternatively, you can also run MindsDB in a docker container assuming that you have [docker](https://docs.docker.com/install/) installed in your computer. Run following commands to pull and run our latest image:

```
docker pull mindsdb/mindsdb
docker run -p 47334:47334 -p 47335:47335 -p 47336:47336 mindsdb/mindsdb
```

## Try out using GoogleCollab

Checkout [![Google Colab](https://colab.research.google.com/assets/colab-badge.svg "MindsDB")](https://colab.research.google.com/drive/1qsIkMeAQFE-MOEANd1c6KMyT44OnycSb) this example on GoogleCollab.

## Hardware

Due to the fact that pytorch only supports certain instruction sets, mindsdb can only use certain types of GPUs.
Currently, on AWS, `g3` and `p3` instance types should be fine, but `p2` and `g2` instances are not supported.
VPS on DigitalOcean with 3 GB Memory and above should work.


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

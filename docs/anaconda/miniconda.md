---
title: Miniconda
---

Miniconda is a free minimal installer for conda. It is a small,
bootstrap version of Anaconda that includes only conda, Python, the
packages they depend on, and a small number of other useful packages,
including pip, zlib and a few others. Use the `conda install command` to
install 720+ additional conda packages from the Anaconda repository.

[See if Miniconda is right for
you](https://docs.conda.io/projects/conda/en/latest/user-guide/install/download.html#anaconda-or-miniconda).

Windows installers
==================

MacOSX installers
=================

Linux installers
================

Installing
==========

-   See hashes for all Miniconda installers &lt;../miniconda\_hashes&gt;.
-   [Verify your
    installation](https://conda.io/projects/conda/en/latest/user-guide/install/download.html#cryptographic-hash-verification).
-   [Installation
    instructions](https://conda.io/projects/conda/en/latest/user-guide/install/index.html).

Other resources
===============

> -   [Miniconda with Python 3.7 for Power8 &
>     Power9](https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-ppc64le.sh)
> -   [Miniconda with Python 2.7 for Power8 &
>     Power9](https://repo.anaconda.com/miniconda/Miniconda2-latest-Linux-ppc64le.sh)
> -   [Miniconda Docker images](https://hub.docker.com/r/continuumio/)
> -   [Miniconda AWS
>     images](https://aws.amazon.com/marketplace/seller-profile?id=29f81979-a535-4f44-9e9f-6800807ad996)
> -   [Archive and MD5 sums for the
>     installers](https://repo.anaconda.com/miniconda/)
> -   [conda change
>     log](https://conda.io/projects/continuumio-conda/en/latest/release-notes.html)
>
> These Miniconda installers contain the conda package manager and
> Python. Once Miniconda is installed, you can use the conda command to
> install any other packages and create environments, etc. For example:
>
>     $ conda install numpy
>     ...
>     $ conda create -n py3k anaconda python=3
>     ...
>
> There are two variants of the installer: Miniconda is Python 2 based
> and Miniconda3 is Python 3 based. Note that the choice of which
> Miniconda is installed only affects the root environment. Regardless
> of which version of Miniconda you install, you can still install both
> Python 2.x and Python 3.x environments.
>
> The other difference is that the Python 3 version of Miniconda will
> default to Python 3 when creating new environments and building
> packages. So for instance, the behavior of:
>
>     $ conda create -n myenv python
>
> will be to install Python 2.7 with the Python 2 Miniconda and to
> install Python 3.7 with the Python 3 Miniconda. You can override the
> default by explicitly setting `python=2` or `python=3`. It also
> determines the default value of `CONDA_PY` when using `conda build`.
>
> > **note**
> >
> > If you already have Miniconda or Anaconda installed, and you just
> > want to upgrade, you should not use the installer. Just use
> > `conda update`.
>
> For instance:
>
>     $ conda update conda
>
> will update conda.

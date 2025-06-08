# Building conda packages from scratch

This tutorial describes how to build a conda package for Click by
writing the required files in the conda build recipe.

## Who is this for?

This tutorial is for Windows, macOS, and Linux users who wish to
generate a conda package by writing the necessary files. Prior knowledge
of conda build and conda recipes is helpful.

## Before you start

-   You should have already completed [Building skeleton packages](build-pkgs-skeleton.md)

## Editing the meta.yaml file

1.  Make a new directory for this tutorial named `click`, and then
    change to the new directory:

    ``` bash
    mkdir click
    cd click
    ```

2.  To create a new `meta.yaml` file, open your favorite editor. Create
    a text file and insert the information shown below. A blank
    sample `meta.yaml` follows the table to make it easier to match up
    the information.

    !!! note
        To allow correct sorting and comparison, specify `version` as a string.

    |  |  |
    |---|---|
    | name | click |
    | version | "7.0" (or latest from [click releases](https://github.com/pallets/click/releases))
    | git_rev |  6.7  (or latest from [click releases](https://github.com/pallets/click/releases))
    | giv_url | <https://github.com/pallets/click.git> |
    | imports | click |
    | home | <https://github.com/pallets/click> |
    | license | BSD |

### Sample meta.yaml

``` yaml
package:
    name:
    version:

source:
    git_rev:
    git_url:

requirements:
    build:
    - python
    - setuptools

    run:
    - python

test:
    imports:

about:
    home:
```

Save the file in the same `click` directory as `meta.yaml`. 
## Writing the build script files build.sh and bld.bat

Besides `meta.yaml`, 2 files are required for a build:

-  `build.sh` Shell script for macOS and Linux.
-  `bld.bat` -Batch file for Windows.

The 2 files `build.sh` and `bld.bat` must be in the
same directory as your `meta.yaml` file.

This tutorial describes how to make both `build.sh` and `bld.bat` so
that other users can build the appropriate package for their
architecture.

1. Open a text editor and create a new file named `bld.bat`. Enter the text exactly as shown:

    ``` bash
    "%PYTHON%" setup.py install
    if errorlevel 1 exit 1
    ```
    !!! note

        In `bld.bat`, the best practice is to to add
        `if errorlevel 1 exit 1` after every command so that if the command
        fails, the build fails.


2.  Save this new file `bld.bat` to the same directory where you put
    your `meta.yaml` file.

3.  Open a text editor and create a new file named `build.sh`. Enter the
    text exactly as shown:

    ``` bash
    $PYTHON setup.py install     # Python command to install the script.
    ```

4.  Save your new `build.sh` file to the same directory where you put
    the `meta.yaml` file.

You can run `build.sh` with `bash -x -e`. The `-x` makes it echo each
command that is run, and the `-e` makes it exit whenever a command in
the script returns nonzero exit status. If you need to revert this in
the script, use the `set` command in `build.sh`.

## Building and installing 

Now that you have your 3 new build files ready, you are ready to create
your new package with conda build and install the package on your local
computer.

1.  Run conda build:

    ``` bash
    conda-build click
    ```

    If you are already in the click folder, you can type
    `conda build .`

    When conda build is finished, it displays the package filename and
    location. In this case the file is saved to:

    ``` bash
    ~/anaconda/conda-bld/linux-64/click-7.0-py37_0.tar.bz2
    ```

    !!! note

        Save this path and file information for the next task. The exact
        path and filename will vary depending on your operating system and
        whether you are using Anaconda or Miniconda. The `conda-build`
        command tells you the exact path and filename.


2.  Install your newly built program on your local computer by using the
    `use-local` flag:

    ``` bash
    conda install --use-local click
    ```

    If there are no error messages, Click installed successfully.

## Converting a package to use on all platforms

Now that you have built a package for your current platform with conda
build, you can convert it for use on other platforms by using the 2
build files, `build.sh` and `bld.bat`.

Use the `conda convert` command with a platform specifier from the list:

-   `osx-64`
-   `linux-32`
-   `linux-64`
-   `win-32`
-   `win-64`
-   `all`

!!! example

    To use the platform specifier `all`:

    ``` bash
    conda convert --platform all ~/anaconda/conda-bld/linux-64/click-7.0-py37_0.tar.bz2 -o outputdir/
    ```

!!! note
    Change your path and filename to the path and filename you saved in [Building and installing](#building-and-installing).

## Using PyPI as the source instead of GitHub

You can optionally use PyPI or another repository instead of GitHub. There is
little difference to conda build between building from Git versus
building from a tarball on a repository like PyPI. Because the same
source is hosted on PyPI and GitHub, you can easily find a script on
PyPI instead of GitHub.

Replace this `source` section:

``` bash
git_rev: v0.6.7
git_url: https://github.com/pallets/click.git
```

With the following:

``` bash
url: https://files.pythonhosted.org/packages/f8/5c/f60e9d8a1e77005f664b76ff8aeaee5bc05d0a91798afd7f53fc998dbc47/Click-7.0.tar.gz
sha256: 5b94b49521f6456670fdb30cd82a4eca9412788a93fa6dd6df72c94d5a8ff2d7
```

!!! note

    The `url` and `sha256` are found on the [PyPI Click
    page](https://pypi.org/project/click/#files).


## Uploading new packages to Anaconda.org

After converting your files for use on other platforms, you may choose
to upload your files to Anaconda.org, formerly known as binstar.org. It
only takes a minute to do if you have a free Anaconda.org account.

1.  If you have not done so already, open a free Anaconda.org account
    and record your new user name and password.

2.  Run the command `conda install anaconda-client`, and then enter your
    Anaconda.org username and password.

3.  Log into your [Anaconda.org](http://anaconda.org) account with the
    command:

    ``` bash
    anaconda login
    ```

4.  Upload your package to Anaconda.org:

    ``` bash
    anaconda upload ~/miniconda/conda-bld/linux-64/click-7.0-py37_0.tar.bz2
    ```

    !!! note
        Change your path and filename to the path and filename you saved in [Building and installing](#building-and-installing)

    !!! Tip

        To save time, you can set conda to always upload a successful build to Anaconda.org with the command: `conda config --set anaconda_upload yes`.

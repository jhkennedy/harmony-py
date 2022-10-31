# harmony-py

Harmony-Py is a Python library for integrating with NASA's [Harmony](https://harmony.earthdata.nasa.gov/) Services.

Harmony-Py provides a Python alternative to directly using [Harmony's RESTful API](https://harmony.earthdata.nasa.gov/docs/api/). It handles NASA [Earthdata Login (EDL)](https://urs.earthdata.nasa.gov/home) authentication and optionally integrates with the [CMR Python Wrapper](https://github.com/nasa/eo-metadata-tools) by accepting collection results as a request parameter. It's convenient for scientists who wish to use Harmony from Jupyter notebooks as well as machine-to-machine communication with larger Python applications.

Harmony-Py is a work-in-progress, is not feature complete, and should only be used if you would like to test its functionality. We welcome feedback on Harmony-Py via [GitHub Issues](https://github.com/nasa/harmony-py/issues)

![Python package](https://github.com/nasa/harmony-py/workflows/Python%20package/badge.svg)

[![Documentation Status](https://readthedocs.org/projects/harmony-py/badge/?version=latest)](https://harmony-py.readthedocs.io/en/latest/?badge=latest)

# Using Harmony Py

## Prerequisites

* Python 3.7+


## Installing

The library is available from [PyPI](https://pypi.org/project/harmony-py/) and can be installed with pip:

        $ pip install -U harmony-py

This will install harmony-py and its dependencies into your current Python environment. It's recommended that you install harmony-py into a virtual environment along with any other dependencies you may have.


# Running Examples & Developing on Harmony Py

## Prerequisites

* Python 3.7+, ideally installed via a virtual environment


## Installing Development & Example Dependencies

1. Install dependencies:

        $ make install

2. Optionally register your local copy with pip:

        $ pip install -e ./path/to/harmony_py


## Running the Example Jupyter Notebooks

Jupyter notebooks in the `examples` subdirectory show how to use the Harmony Py library. Start up the Jupyter Lab notebook server and run these examples:

The Jupyter Lab server will start and [open in your browser](http://localhost:8888/lab). Double-click on a notebook in the file-browser sidebar and run the notebook. Note that some notebooks may have cells which prompt for your EDL username and password. Be sure to use your UAT credentials since most of the example notebooks use the Harmony UAT environment.

        $ make examples


## Developing

### Generating Documentation

Documentation on the Read The Docs site is generated automatically. It is generated by using `sphinx` with reStructuredText (.rst) and other files in the `docs` directory. To generate the docs locally and see what they look like:

        $ make docs

You can then view the documentation in a web browser under `./docs/_build/html/index.html`.

IMPORTANT: The documentation uses a notebook from the `examples` directory rendered as HTML. If you've modified that notebook (see `Makefile` for notebook that is currently rendered), you will need to run `make docs` locally. You will see a change to the `docs/user/notebook.html` file after doing so. This file should be committed to the git repo since it is used when the latest docs are pushed to the Read The Docs site (it can't currently be generated as part of the build).

### Running the Linter & Unit Tests

Run the linter on the project source:

        $ make lint

Run unit tests and test coverage. This will display terminal output and generate an HTML coverage report in the `htmlcov` directory.

        $ make test

For development, you may want to run the unit tests continuously as you update tests and the code-under-test:

        $ make test-watch


### Generating Request Parameters

The `harmony.Request` constructor can accept parameters that are defined in the [Harmony OGC API schema](). If this schema has been changed and the `Request` constructor needs to be updated, you may run the generator utility. This tool reads the Harmony schema and generates a partial constructor signature with docstrings:

        $ python internal/genparams.py ${HARMONY_DIR}/app/schemas/ogc-api-coverages/1.0.0/ogc-api-coverages-v1.0.0.yml

Either set `HARMONY_DIR` or replace it with your Harmony project directory path. You may then write standard output to a file and then use it to update the `harmony.Request` constructor and code.

## CI

Harmony-py uses [GitHub
Actions](https://github.com/nasa/harmony-py/actions) to run the Linter
& Unit Tests. The test coverage output is saved as a build artifact.

## Building and Releasing

New versions of Harmony-Py will be published to PyPi via a GitHub [action](.github/workflows/publish-release.yml) whenever a draft release is marked as published https://github.com/nasa/harmony-py/releases.

# Chroma Server

## Development

Set up a virtual environment and install the project's requirements
and dev requirements:

```
python3 -m venv venv      # Only need to do this once
source venv/bin/activate  # Do this each time you use a new shell for the project
pip install -r requirements.txt
pip install -r requirements_dev.txt
```

To run tests, run `bin/test`. This will run the test suite inside a
docker compose cluster, with the database available, and clean up when complete.

To run the server locally, in development mode, run `uvicorn chroma_server:app --reload`

## Docker

To build the docker image locally, run `bin/build`.

The version tag of the build is generated by the `bin/version` script,
which uses the `setuptools_scm` library. For full documentation, see
the
[documentation for setuptools_scm](https://github.com/pypa/setuptools_scm/).

In brief, version numbers are generated as follows:

- If the current git head is tagged, the version number is exactly the
  tag (e.g, `0.0.1`).
- If the the current git head is a clean checkout, but is not tagged,
  the version number is a patch version increment of the most recent
  tag, plus `devN` where N is the number of commits since the most
  recent tag. For example, if there have been 5 commits since the
  `0.0.1` tag, the generated version will be `0.0.2-dev5`.
- If the current head is not a clean checkout, a `-dirty` local
  version will be appended to the version number. For example,
  `0.0.2-dev5-dirty`.

To run use `docker images` to see what containers and tags you have available:
```
docker run -p 8000:8000 ghcr.io/chroma-core/chroma-server:<tag name -- eg 0.0.2-dirty>>
```

This will expose the internal app at `localhost:8000`
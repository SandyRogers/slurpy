# Slurpy (SLUrm rest api PYthon client)
Slurpy is a Python client for the [Slurm REST API](https://slurm.schedmd.com/rest.html).
Slurm is an open-source job scheduler for high performance compute environments.
Its REST API is a set of HTTP endpoints for submitting, monitoring, and managing compute jobs.
This Python client is a convenience library for interacting with that API.

## Development
### Requirements
* [poetry](https://python-poetry.org/docs/#installation)
* Docker / compose (via any means... docker, podman, colima etc).

### Setup
```shell
poetry install
poetry run pre-commit install
```

### Running in dev mode
This repo includes a docker-compose containerised minimal slurm cluster, for dev work.
It just runs two containers: a maria DB for slurm job persistence, and a single node of a slurm compute cluster.
The single node is running the slurm controller, the slurm database daemon, the slurm rest API daemon, and a slurm worker node daemon.
This can be broken up into multiple containers, so that e.g. the controller, rest server, and workers are all separate "nodes", but it makes the dev env a lot heavier.
This is all in the `slurm-in-docker/` dir.
```shell
docker compose -f slurm-in-docker/docker-compose.yaml up  # starts a single-node slurm cluster and db controller in docker
```

### Tests
TODO

Should use `pytest`, and have github actions workflow.
We should mock the Slurm REST API for most tests.
We may want a couple of e2e/integration tests that run the dockerized slurm cluster, but not necessarily.

### Release to PyPI
TODO

Should use `poetry publish`.

### Semi-automatic generation of the client
IDEA
* Use [datamodel-code-generator](https://docs.pydantic.dev/latest/integrations/datamodel_code_generator/) to convert the desired Slurm REST API Openapi schema into Pydantic models.
* Curate the `model.py` into a more pleasant scheme.
* Probably keep the auto-generated `model.py` files around so that we can git-diff between versions to work out how to update the curated model.  


## Usage
### As a library
TODO

### As a CLI
TODO

IDEA: use textual to add a CLI/TUI option for monitoring (and maybe submitting) jobs.
See [mjobs](https://github.com/mberacochea/mjobs) for inspiration.
This should be available as an add-on package, e.g. `pip install slurpy[cli]`.
Use [poetry extras](https://python-poetry.org/docs/pyproject/#extras) for this.
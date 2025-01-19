# Uncommon Dockerfile Bug

This repository demonstrates a common but subtle error in Dockerfiles: using `ubuntu:latest` and an incorrect order of instructions when installing dependencies.

## The Bug

The original `Dockerfile` uses `ubuntu:latest`, which is bad practice because it can lead to unexpected changes in behavior across builds.  The `requirements.txt` is also added after other files, which means pip will fail to install the necessary packages.

## The Solution

The fixed `Dockerfile_fixed` addresses these issues by:

1. Specifying a specific version of Ubuntu, ensuring reproducibility.
2. Copying `requirements.txt` before other files to correctly resolve dependencies.

## How to Reproduce

1. Clone this repository.
2. Build the original Dockerfile: `docker build -t buggy-app .` (This will likely fail)
3. Build the fixed Dockerfile: `docker build -t fixed-app -f Dockerfile_fixed .` (This should succeed)


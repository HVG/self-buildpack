# HVG / self-buildpack

## What is Buildpacks

Buildpacks are the scripts that power app builds on [Heroku](https://www.heroku.com/). Check out the [Buildpacks article](https://devcenter.heroku.com/articles/buildpacks) for an overview of what role buildpacks play on the Heroku platform or check out the [Buildpack API article](https://devcenter.heroku.com/articles/buildpack-api) to understand how buildpacks work.

## What is Self-buildpack

This buildpack was originally designed to run build srcript inside the application repository. The idea is that you have an application in your repository with own build environment and script (e.g. `Makefile`) to compile your application on self (aka self-buildpack).

## Usage (Typical use case)

Create a directory for our Heroku App:

```bash
$ mkdir app && cd app
```

Create a simple binary to run our Heroku App build:

```bash
$ echo -e "#\!/usr/bin/env bash\n echo Building ..." > ./build.sh
$ chmod +x ./build.sh
$ ./build.sh
Building ...
```

Create an `bin` folder with 'compile' for standard entry point for build process:

```bash
$ mkdir ./bin
$ echo -e "#\!/usr/bin/env bash\n eval \$1/build.sh" > ./bin/compile
$ chmod +x ./bin/compile
```

Create an app with the Self Buildpack:

```bash
$ git init; git add .; git commit -am 'init'
$ heroku create --buildpack https://github.com/hvg/self-buildpack.git
$ git push heroku +HEAD:master
```

The output of the build proccess:

```txt

```

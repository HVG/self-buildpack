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

Create an `bin` folder with `compile` for standard entrypoint of build process:

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
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (5/5), 364 bytes | 364.00 KiB/s, done.
Total 5 (delta 0), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Self Buildpack app detected
remote:        Calling 'compile' task
remote: Building ...
remote: -----> Discovering process types
remote:        Procfile declares types -> (none)
remote:
remote: -----> Compressing...
remote:        Done: 245B
remote: -----> Launching...
remote:        Released v3
remote:        https://fast-earth-75240.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/fast-earth-75240.git
 * [new branch]      HEAD -> master
```

**That's It**
...

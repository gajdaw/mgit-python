# mgit

This script helps to run the same git commands
in multiple repositories.

For example, if you want to checkout `abc` branch in all the repos,
then all you need to run is

    mgit checkout abc

## Install

Clone the repo:

    git clone git@github.com:gajdaw/mgit-python.git

Install dependencies:

    pip3 install -r requirements.txt

Create symbolic link to `main.py` file:

    cd ~/bin
    ln -s /path/to/the/repo/mgit-python/main.py mgit

I assume that `~/bin` directory is included in your `PATH`.

## Configure

Configuration is optional.
`mgit` can work with multiple git repositories cloned to one directory without any configuration file.

Remember, that without configuration file:
- you cannot clone repos using `mgit` (you must clone repos with `git clone` commands)
- you cannot use tags

If you want to use configration file then
create the file named `mgit.yaml` and fill it with information about
repositories that you want to work with, for example:

    # mgit.yaml
    dir: "../../tmp"
    baseUrl: git@github.com:PragmaticGuideToTheCloud/{{name}}.git

    repos:

      - name: mgit
        tags:
          - product

      - name: gitignore
        url: git@github.com:github/gitignore.git
        tags:
          - two

The file may be located anywhere on your filesystem.

The command `mgit` should be executed in the directory, where `mgit.yaml` file is located.

Verify the configuration with:

    mgit debug

The command dumps the configuration to stdout.

## Commands

Print help:

    mgit

Check configuration:

    mgit debug

Check status of all repositories:

    mgit status

Change branches in all repositories:

    mgit checkout master

Run generic git command or git alias in all repositories:

    # l is an alias to git log --oneline
    mgit git "l -1"

## Unit tests

    pytest test*.py

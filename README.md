# gitman

## Introduction

Git utility for managing multiple repositories.  It operates using a manifest file, `.gitmanrc`, which contains all the necessary configuration.

## Install

To install globally:

    $ npm install -g gitman

## Usage

Run `gitman` using the binary, e.g.:

```shell
$ gitman -h
  git utility for managing multiple repositories

  Usage: gitman <options> <commands>

  Options:
    -h, --help                  output usage information
    -p, --pattern <pattern>     pattern to match
    -v, --verbose               verbose output

  Commands:
    init                        creates .gitmanrc in the current directory
    list                        list repositories by full name
    json                        outputs repositories in json format
    manage                      manages repositories, cloning and setting remotes as necessary
```

gitman traverse up from the current working directory till it finds a `.gitmanrc` file containing configuration in JSON.

A sample configuration for this project might be:

```JSON
{
  "repos": [
    {
      "fullName": "krisb/gitman",
      "group": "krisb",
      "name": "gitman",
      "path": "dev/krisb/gitman",
      "remotes": {
        "origin": "git@github.com:krisb/gitman.git"
      }
    }
  ]
}
```

## Design Notes

### libgit2 vs exec

libgit2 support in node is lacking.  <https://github.com/libgit2/node-gitteh> is in need of a new owner and <https://github.com/nodegit/nodegit> doesn't support git over ssh.

For now, this relies on child process exec.

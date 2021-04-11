---
date: "2018-04-09T00:00:00Z"
title: Pointers for Pipenv
---

Pipenv is a great tool to use, read more about pipenv <a href="https://github.com/pypa/pipenv">**HERE**</a>.

Pipenv generated a lock file that is useful in replicating an exact virutal environment, which can be useful in a lot of cases.

The best way to install pipenv is to install it using pip but locally, so that all the pipenv environments are also in the .local/ folder inside the user directory.

{{< highlight shell >}}
pip install -U pipenv

{{< / highlight >}}


Pipenv works with pew ([read more about pew here](https://github.com/berdario/pew)) to create the virtual environments.

Though pipenv provides the ability to store the virtual environment inside the project folder by setting the *VENV_IN_PROJECT* environment variable, I prefer not using it like that. There are a couple of benefits to this -

   1. This allows me to keep the codebase isolated from the runtime environment and simply zipping up the code is a much easier process.

   2. Having the virtual environment inside the home directory of the user allows for scheduling cron jobs using the user space where the cron job is consequently able to find the virtual environment.

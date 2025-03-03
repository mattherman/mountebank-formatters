# Project Status

This repository is a fork of [bbyars/mountebank-formatters](https://github.com/bbyars/mountebank-formatters). See the project status in the [mattherman/mountebank](https://github.com/mattherman/mountebank?tab=readme-ov-file#project-status) for more information.

# Formatters

As of v2.4.0, [mountebank](https://github.com/mattherman/mountebank) supports custom formatters.

A formatter consists of two functions:
* `load`, which loads the `--configfile` used to start mountebank
* `save`, which saves the test data captured in a running process of mountebank using the `mb save` command

Those two functions should work in concert, so you can round-trip the configuration. In other words, the
following should always work for the same formatter:

````
mb save --savefile mb.json --formatter path/to/customFormatter
mb restart --configfile mb.json --formatter path/to/customFormatter
````

For years, mountebank supported EJS templating, which could be turned off using the `--noParse` CLI flag.
When EJS made a breaking change, mountebank couldn't accept it because it would break existing config files.
That has now been modularized into this module (allowing mountebank core to upgrade EJS), and remains
the default option for backwards compatibility. However, now mountebank supports configurable formatters.

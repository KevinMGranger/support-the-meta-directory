# Respect The Meta Directory.
Please!

Work in progress, more content coming soon.

The idea behing this movement is to combat the overwhelming amount of top-level project configuration files.

Although having these standardized tools supported in projects is a good thing, it leaves the project looking cluttered, especially when viewing it for the first time on something like GitHub or GitLab.

This proposal asks that these tools also check a top-level `meta` directory, which can hold these files as well.

There would be a single exception of a top-level `metameta`, which would contain the name of a single "fallback" folder to use instead for cases where tools or standards dictate that there would be a top-level directory named `meta` for other purposes. 

For example, python packages typically have a top-level directory with the same name as the package, so a python package called `meta` would need a fallback to something else. This top-level fallback could have a sensible default, perhaps making `metameta` unnecessary.

# Respect The Meta Directory.
Please!

Work in progress, more content coming soon.

The idea behing this movement is to combat the overwhelming amount of top-level project configuration files.

Although having these standardized tools supported in projects is a good thing, it leaves the project looking cluttered, especially when viewing it for the first time on something like GitHub or GitLab.

This proposal asks that these tools also check a top-level `meta` directory, which can hold these files as well.

There would be a single exception of a top-level `metameta`, which would contain the name of a single "fallback" folder to use instead for cases where tools or standards dictate that there would be a top-level directory named `meta` for other purposes. 

For example, python packages typically have a top-level directory with the same name as the package, so a python package called `meta` would need a fallback to something else. This top-level fallback could have a sensible default, perhaps making `metameta` unnecessary.

If you'd like to contribute towards this writeup / standard / list of tools that should support it, do so [here](https://github.com/KevinMGranger/respect-the-meta-directory)

<a href="https://github.com/KevinMGranger/respect-the-meta-directory"><img style="position: absolute; top: 0; left: 0; border: 0;" src="https://camo.githubusercontent.com/c6625ac1f3ee0a12250227cf83ce904423abf351/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f6c6566745f677261795f3664366436642e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_left_gray_6d6d6d.png"></a>

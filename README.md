# Let's unclutter everyone's repos: support the Meta Directory!

There seems to be a trend of projects having a high amount of configuration
files living in the top of the repo.

I do not bring this up to shame project that have these files-- quite the
opposite: supporting a myriad of developer tools can help ease adoption for the
project.

However, when a project is encountered for the first time on a site like GitHub
or GitLab, a visitor's first sight should be information about the project, not
how many CI tools it supports. These files wind up making a lot of noise at the
top level, distracting from the more important (to a first-timer) documentation
such as README, CONTRIBUTING/HACKING, BUILDING, and LICENSE files.

The proposed fix is simple: have these tools check for their config files at the
top level as usual, but secondarily check the top-level directory called `meta`.

For projects / tools that need to have a top-level `meta` folder for some other
reason, a top-level `metameta` file can contain the name of another directory to
fall back to. This should be rare.

For example, python packages typically have a top-level directory with the same
name as the package, so a python package called `meta` would need a fallback to
something else.

<!-- TOC -->

- [Let's unclutter everyone's repos: support the Meta Directory!](#lets-unclutter-everyones-repos-support-the-meta-directory)
    - [The Meta Directory Standard](#the-meta-directory-standard)
    - [The Meta Directory Standard tl;dr version](#the-meta-directory-standard-tldr-version)
    - [History / Prior Art / Inspirations](#history--prior-art--inspirations)
        - [Dotfiles: the bug that became a feature](#dotfiles-the-bug-that-became-a-feature)
        - [The XDG .config directory](#the-xdg-config-directory)
    - [Counter-arguments](#counter-arguments)
    - [Contributing](#contributing)
    - [Tools That Should Implement This](#tools-that-should-implement-this)
        - [CI](#ci)
        - [Language-Specific](#language-specific)
        - [Editing / Text Tools](#editing--text-tools)
        - [Other General Dev Tools](#other-general-dev-tools)
    - [Projects that would benefit from this](#projects-that-would-benefit-from-this)

<!-- /TOC -->


## The Meta Directory Standard

The key words “**MUST**”, “**MUST** **NOT**”, “**REQUIRED**”, “**SHALL**”,
“**SHALL** **NOT**”, “**SHOULD**”, “**SHOULD** **NOT**”, “**RECOMMENDED**”,
“**MAY**”, and “**OPTIONAL**” in this document are to be interpreted as
described in RFC 2119.

1. If the file `metameta` exists in the root of the repository, then the
   contents of the file **SHALL** be interpreted as the "Meta Directory", as a
   path relative to the root of the repository.

2. If the file `metameta` does not exist in the root of the repository, then the
   directory `meta` in the root of the repository **SHALL** be the "Meta
   Directory".

3. A tool which typically looks for a configuration file or directory in the
   root of the repository **SHALL** look for that file or directory first, and
   if it is not found, look in the Meta Directory for that file or directory.

4. A tool **MUST NOT** treat the presence of a configuration file or directory
   in both the root of the repository and in the Meta Directory as an error. It
   **MAY** treat it any other way; e.g. one may supersede the other, or one may
   augment the other.

5. A tool **MAY** encourage the use of the Meta Directory over the top level.

6. A tool **SHOULD NOT** chose to support solely the Meta Directory and not the
   root of the repo if it has already had a "major" (in terms of SemVer
   compatibility) release that supported the root.


## The Meta Directory Standard tl;dr version

The meta dir is the dir named in `metameta` if `metameta` is there, or else it's
`meta`.

If your tool has a config file in the root of the repo, check for that first,
then check the meta dir second if it isn't there.

If the config is in both places, you can't treat that as an error, but you can
treat that any other way.

If you already had a major release that checked the top level, try not to remove
support for that. You're allowed to _encourage_ using the meta dir, though.


## History / Prior Art / Inspirations

### Dotfiles: the bug that became a feature

Rob Pike, a programmer best known (in this context) for his work on Unix and
Plan 9, shared [a story on Google+ back in
2012](https://plus.google.com/u/0/+RobPikeTheHuman/posts/R58WgWwN9jp) about "A
lesson in shortcuts."  Unix added the `.` and `..` entries in directory
listings. They wanted these hidden when one typed `ls`. So, they checked if the
first character of a filename was `.`

Rob said the rest the best himself:

> ...the idea of a "hidden" or "dot" file was created. As a consequence, more lazy programmers started dropping files into everyone's home directory. I don't have all that much stuff installed on the machine I'm using to type this, but my home directory has about a hundred dot files and I don't even know what most of them are or whether they're still needed. Every file name evaluation that goes through my home directory is slowed down by this accumulated sludge.

> I'm pretty sure the concept of a hidden file was an unintended consequence. It was certainly a mistake.

> ...

> (For those who object that dot files serve a purpose, I don't dispute that but counter that it's the files that serve the purpose, not the convention for their names. They could just as easily be in $HOME/cfg or $HOME/lib, which is what we did in Plan 9, which had no dot files. Lessons can be learned.)

To summarize: dotfiles were a *bug*. There should have been a "top-level" (to
the user's home) directory to hold configuration files, and said directory was
added in Plan 9. Plan 9 was essentially Unix done better, after all.

### The XDG .config directory

[The XFG Base Directory
Specification](https://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html),
a specification that came out of a grou project interoperability between desktop
environments, specifies that:

> there is a single base directory relative to which user-specific configuration files should be written.

The default is `$HOME/.config`, but it is also configurable.


## Counter-arguments

For fairness's sake, let's collect the common counter-arguments to this proposal here:

1. **The presence of language-specific tooling files quickly identifies what
   language the project uses.** While this is true, GitHub offers an excellent
   summary of what langauges are used at the top of the repo, and any project
   that has both a frontend and backend component in the same repo makes this
   harder to immediately identify anyway. But as a compromise, perhaps the
   essential lang-specific files (e.g. Cargo.toml, package.json, setup.py) could
   or should stay at the top level.
   
   
## Contributing

The most effective way to have this be adopted is for you to contribute towards
these tools in the way they ask for folks to contribute-- if that's just showing
up with code, then please do that. If that's asking about their development
process and integrating with the community first, then do that. And if you like
that project overall, why not stay, eh?

If you'd like to contribute towards this writeup / standard / list of tools that i
should support it, do so
[here](https://github.com/KevinMGranger/support-the-meta-directory).

You can suggest changes to the above writeup, or add entries to the lists of
tools that should implement this, or list of projects that would benefit from
this.

The only request is that you keep this markdown file clean (line-broken at 81
chars except for quotes and tables, and the tables properly aligned). I recommend Visual Studio Code with the
plugins Rewrap and markdown Table Prettifier.

Or if you just file an issue, I'll add it if accepted.


## Tools That Should Implement This

In the status column:

For the idea:

TBP: To be proposed. Has not been suggested to the project yet.

ID: In discussion. Those involved with the project are discussing it.

WONTFIX: Idea rejected.

GO: Idea accepted, work remaining.

MAYBE: Idea entertained but does not have full support, work remaining.

NP: Will not be proposed. We do not think it will be adopted, or is a good fit
for the project.

For the work:

PS: Patch submitted. A patch adding support for the meta directory has been
submitted.


### CI

Name      | Filename     | Status
----------|--------------|--------
Appveyor  | appveyor.yml | TBP
Travis CI | .travis.yml  | TBP
GitLab CI | TODO         | TBP
Code Climate | .codeclimate.yml | TBP

### Language-Specific

Language | Tool Name   | Filename         | Status | Description
---------|-------------|------------------|--------|------------------------
Python   | setuptools  | setup.py         | TBP    |
Python   | pip         | requirements.txt | TBP    |
Python   | TODO        | setup.cfg        | TBP    |
Python   | tox         | tox.ini          | TBP    |
Python   | pylint      | .pylintrc        | TBP    |
Python   | coverage.py | .coveragerc      | TBP    |
Ruby     | gem         | Gemfile          | TBP    |
Ruby     | gem         | Gemfile.lock     | TBP    |
Ruby     | Rake        | Rakefile         | TBP    |
Ruby     | gem         | $NAME.gemspec    | TBP    |
Ruby     | rubocop     | .rubocop.yml     | TBP    |
Ruby     | rspec       | .rspec           | TBP    |
Ruby     | rvm         | .rvmrc           | TBP    |
Ruby     | rvm         | .versions.conf   | TBP    |
Ruby     | rvm         | .ruby-version    | TBP    |
Ruby     | capistrano  | Capfile          | TBP    |
Ruby     | rack        | config.ru        | TBP    |
TODO     | TODO        | Dangerfile       | TBP    |
Rust     | cargo       | Cargo.toml       | TBP    |
Rust     | cargo       | Cargo.lock       | TBP    |
C/C++    | Make        | Makefile         | NP     | The classic build tool
C++      | CMake       | CMakeLists.txt   | TBP    | The build tool builder
JS       | babel       | .babelrc         | TBP    |
JS       | eslint      | .eslintignore    | TBP    |
JS       | eslint      | .eslintrc.yml    | TBP    |
JS       | NVM         | .nvmrc           | TBP    |
JS       | npm         | package.json     | TBP    |
JS       | yarn        | yarn.lock        | TBP    |

### Editing / Text Tools

Name         | Filename       | Status | Description
-------------|----------------|--------|------------------------------------------
EditorConfig | .editorconfig  | TBP    | A standardized editor configuration file
Haml         | .haml-lint.yml | TBP    |
SCSS-lint    | .scss-lint.yml | TBP    |

### Other General Dev Tools

Name    | Filename           | Status | Description
--------|--------------------|--------|-------------------------------------------------------------
git     | .gitignore         | TBP    | A list of files to ignore from consideration for committing
git     | .gitattributes     | TBP    | A list of attributes for the repo.
just    | justfile           | TBP    | Just a command runner
docker  | Dockerfile         | TBP    |
docker  | .dockerignore      | TBP    |
docker  | docker-compose.yml | TBP    |
heroku  | .buildpacks        | TBP    |
heroku  | .slugignore        | TBP    |
heroku  | Procfile           | TBP    |
heroku  | app.json           | TBP    |
foreman | .foreman           | TBP    |
nanobox | .nanoignore        | TBP    |
nanobox | boxfile.yml        | TBP    |
vagrant | Vagrantfile        | TBP    |


## Projects that would benefit from this

**This is not a wall of shame.**

As said above, if a project is listed here,
that means it has gone above and beyond supporting the vibrant ecosystem of
developer tooling, and making it easier for people to use and devleop on their
project. This is simple to illustrate why this standard is necessary, and also
remind us who we can contribute patches towards to help declutter as this
standard is adopted.

Number of Files | Project
----------------|---------------------------------------------------
42              | [Mastodon](https://github.com/tootsuite/mastodon)
18              | [Ansible AWX](https://github.com/ansible/awx)
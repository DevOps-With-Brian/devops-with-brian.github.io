---
title: "Auto Versioning Any Project Using Commitizen & Conventional Commits"
date: 2022-11-20
categories:
  - blog
  - devops
  - commitizen
  - conventional commits
  - auto versioning
tags:
  - devops
  - how-to
  - tutorial
  - versioning
  - conventional commits
toc: true
---

# General Overview
One thing I come across a lot in my different roles has been versioning, and its always something that can be a pain.  Sometimes you have to update multiple files with the version when it changes, docs, etc.

Today we are going to talk about using [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) along with [Commitizen](https://commitizen-tools.github.io/commitizen/) to auto version and create a automated changelog for us.

Conventional Commits is a specification around your commit messages.  You can read more about how conventional commits work at the previous mentioned link.  The general idea though is based on if you do a `feat` or `fix` type of commit it will control how the version is incremented.

Commitizen is a tool we can use to create conventional commits easier as well as auto bump versions and changelog based on the commits.  Ensure you have installed [Commitizen](https://commitizen-tools.github.io/commitizen/) using one of their methods before continuing.

# Auto Versioning Setup
The below steps outline how to get auto versioning setup and working.

## Setup GitHub Repo
The first thing you want to do is setup a new GitHub/GitLab/Etc repo to test this in, we need it to be a git repo for the auto versioning to work and tag correctly.  It uses the tags from git to know how to auto increment based on the commit history.

After cloning your initial repo, (I'd recommend just setting it with a README.md) we can get started.

## Install Commitizen
As mentioned before ensure [Commitizen](https://commitizen-tools.github.io/commitizen/) has been installed.

## Commitizen Init & Bump
Now we can initialize our repo with commitizen using:

`cz init`

This will ask us a few questions we have to answer as you can see in the gif below.  You can use pyproject.toml if you are using python or existing poetry project, and if you don't like toml format you can select a different format.

The beauty of this though is you can literally use this with any type of project.

![CZ Init](/assets/images/cz_init.gif)

Next we have to do the `git tag 0.0.1` to create the initial 0.0.1 version.

![Git Tag](/assets/images/git_tag.gif)

## Generate Changelog
Now we can run the `cz changelog` command to generate a new changelog file.  Then we can add this to version control via `git add .` to add our new `.cz.toml` file and our `CHANGELOG.md` file.

We also can now run `cz c` to generate the menu for us to create a commit and we can select this as a `fix` to show how it will auto update the version from `0.0.1` to `0.0.2`.

![CZ Changelog](/assets/images/cz_change_git_add.gif)

## Commitizen Bump & Push
Now we can do a version bump since we have a new commit, in order to do that and generate the changelog we can do:

`cz bump --changelog`

This will bump the version if the commits call for it and also update the `CHANGELOG.md` accordingly.

We can then just do a `git push origin XXX` where XXX is your branch and push our updates, since it did the version bump for us it will generate the commit and add files.

![CZ Bump](/assets/images/cz_bump_push.gif)

# Updating Versions In Other Files
You are probably saying, ok this is cool and all and can update this one `.cz.toml` file and create a `CHANGELOG.md` file, but what if I want my versions updated in other things?

Well that is easy enough with commitizen as well, if you check out their section in the [Docs](https://commitizen-tools.github.io/commitizen/bump/#version_files) there are options for telling commitizen how to udpate files.

So lets create a my_version.txt file:

`echo "version=0.0.2" > my_version.txt`

Now we should have a file called `my_version.txt` with text in it that says `version=0.0.2`.

So now on a new bump we want commitizen to also update this version number in this file, so the way we can do that is adding the following to our existing `.cz.toml` file:

```toml
[tool.commitizen]
version_files = [
    ".cz.toml",
    "my_version.txt:version"
]
```

So the total file should look like:

```toml
[tool]
[tool.commitizen]
name = "cz_conventional_commits"
version = "0.0.2"
tag_format = "$version"

version_files = [
    ".cz.toml",
    "my_version.txt:version"
]
```

What we are doing here is telling it to obviously keep the .cz.toml file updated, along with the `version` var inside of the `my_version.txt` file.

To test this we can add this file and do a cz bump to watch it update everything:

`git add .` to add our updated `cz.toml` file and our `my_version.txt` file.

Now lets do a `cz c` and select `feat` this time for a different version bump.

Finally lets do a `cz bump --changelog` to bump the version and update the changelog.

```bash
bump: version 0.0.2 → 0.1.0
tag to create: 0.1.0
increment detected: MINOR

[main 3ed7d21] bump: version 0.0.2 → 0.1.0
 3 files changed, 8 insertions(+), 2 deletions(-)

Done!
```

Now if you cat the `.cz.toml` file you will see it has updated:

```toml
[tool]
[tool.commitizen]
name = "cz_conventional_commits"
version = "0.1.0"
tag_format = "$version"

version_files = [
    ".cz.toml",
    "my_version.txt:version"
]
```

And our `version` var in our `my_version.txt` has also updated:

```txt
version=0.1.0
```

What happened here was since we selected a `feat` commit it updated the `MINOR` version location so that is why we went from `0.0.2` to `0.1.0`.

```bash
bump: version 0.0.2 → 0.1.0
tag to create: 0.1.0
increment detected: MINOR

[main 3ed7d21] bump: version 0.0.2 → 0.1.0
 3 files changed, 8 insertions(+), 2 deletions(-)

Done!
```

Here is an example of everything together on the cli:

![CZ Bump](/assets/images/cz_bump_txt_file.gif)

# Final Thoughts & CI Options
So now utilizing the `cz bump` command and Conventional Commits, you can now setup CI to do this process for you.

Typical process would be to validate commit message on PR is a valid conventional commit message, then on merges into your main branch you can generate the `cz bump --changelog` command and update if there is a new version then push this back to the repo.

Hopefully this small tutorial helped and you can look at [Chatbot Auto Version Example](https://github.com/DevOps-With-Brian/chatbot-auto-versioning) by looking at the `.github/workflows` dir.  You can see in the `build-train-pr.yml` how we validate the commit message.

In the `bump_version.yml` you can see how the version is bumped and is then used to version our artifact model file.
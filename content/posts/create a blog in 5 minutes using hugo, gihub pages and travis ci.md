---
title: "Create a blog in 5 minutes using Hugo, GitHub Pages and Travis CI"
date: 2017-10-28
tags: ["Hugo", "Go", "GitHub", "GitHub Pages", "Travis CI", "CI", "CD"]
draft: false
---

## Blog creation

### Install Hugo
[Official documentation](https://gohugo.io/getting-started/installing/) outlines this step for many operating systems very well.

### Create a site
Open command line and run
```
hugo new site blog
```
Initialize a git repository and create a first commit.
```
git init
git commit -m "create a site"
```
 
### Add a theme

Hugo has a lots of [themes](https://themes.gohugo.io/). For example, I use [Minimal](https://themes.gohugo.io/minimal/)

```
git submodule add https://github.com/calintat/minimal.git themes/minimal
```

After installation, take a look at the exampleSite folder inside themes/minimal.

To get started, copy the config.toml file inside exampleSite to the root of your Hugo site.

In addition, I'd recommend to update the config according to your personal info such as email, github username and etc.

### Create a post

```
hugo new post/my-first-post.md
```

Start the hugo server and open your blog locally on [http://localhost:1313](http://localhost:1313).

```
hugo server
```

## Publiching to GitHub Pages and continious delivery

### Push your code to GitHub

Create a new repository on GitHub and push your local repository to the remote rerository.
I have created [blog](https://github.com/Anufriev/blog) repository.

Create a new repository with a special name yourgithubhame.github.io. 
I have created [anufriev.github.io](https://github.com/Anufriev/anufriev.github.io) repository.

### Configure Travis CI

Open [Travis CI](https://travis-ci.org/) and go to the account page.

![Travis CI: enable repository](/posts/create a blog in 5 minutes using hugo, gihub pages and travis ci.travis-enable-repository.PNG)

Click on Sync account button.
You blog repository should be displayed there.

Go to the GitHub developer setting page.

![Travis CI: enable repository](/posts/create a blog in 5 minutes using hugo, gihub pages and travis ci.github-tokens.PNG)

Click on Generate new token button.

![Travis CI: enable repository](/posts/create a blog in 5 minutes using hugo, gihub pages and travis ci.github-tokens-generate.PNG)

Enter name for a new token, grant repo scope and click on Generate button.

![Travis CI: enable repository](/posts/create a blog in 5 minutes using hugo, gihub pages and travis ci.github-tokens-copy.PNG)

Copy the token.

Open Travis CI and go to the setting page of the build of your blog repository.

![Travis CI: enable repository](/posts/create a blog in 5 minutes using hugo, gihub pages and travis ci.travis-add-github-token.PNG)

Add a new environment variable GITGUB_TOKEN and paste the token from clipboard.

Add .travis.yml file to the root of the your blog repository.

```
sudo: true
dist: trusty

install:
  - sudo apt-get --yes install snapd
  - sudo snap install hugo

script:
  - /snap/bin/hugo

# Deploy to GitHub pages
deploy:
  provider: pages   
  skip_cleanup: true  
  github_token: $GITHUB_TOKEN # Set GITHUB_TOKEN in travis-ci.org settings dashboard
  local_dir: public
  repo: Anufriev/anufriev.github.io
  target_branch: master
  
  on:
    branch: master
```

Commit, push, wait a few minutes. 

Open yourgithubname.github.io and enjoy!
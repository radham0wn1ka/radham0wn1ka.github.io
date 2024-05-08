---
layout: post
title:  "git github"
date:   2024-05-08 09:29:20 +0700
categories: git github pull requests
usemathjax: true
---
## outline
- m0wn1ka has a repo named ctf_writeups
- radham0w1na needs to work on the m0wn1ka repo
- radham0wn1ka sends a request with changes made and m0wn1ka checks and then merges the code in m0wn1ka's repo
## process of owner of source repo(m0wn1ka)
- m0wn1ka(p1) has a repo  in github named ctf_writeups
- p1 in local git init,git add . git commit -m "c1" 
- p1 then git branch -M main
- then p1 does creates github access token by developer settings and create a classic token
- git config --global user.email ""
- git config --global user.name ""
- then p1 does git remote set-url origin https://<token>@github.com/username/repo_name
- this creates a link b/w local and remote
- git push -u origin main
## process of contributer (radham0wn1ka)
- radham0wn1ka(p2) goes to the p1's repo in github
- p2 forks p1's repo into p2's  account
- p2 clones the repo which is forked by git clone https://github.com/radham0wn1ka/<forked_name>
- then p2 does the intended changes
- then p2 git pushes
- if it gives error then
```
git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```
- p2 as well creates their own github acces token by 
```
settings->developer setttings->personal access token->token classic->generate a new token
```
- git remote set-url origin https://<token>@github.com/radham0wn1ka/<forked repo name>
- once configurateion is done we git push the code 
- then in github website go to the repo and contribute and pull request
## proces of checking and merging the code by owner(m0wn1ka)
- see that there is a opened pull request
```
 Open
pull request1
#1
radham0wn1ka wants to merge 2 commits into m0wn1ka:main from radham0wn1ka:main
```
- like this it appers to p1
- so we checkout a new branch and pull the new code
```
git checkout -b radham0wn1ka-main main
git pull https://github.com/radham0wn1ka/<forked_repo_name>.git main
```
- then once it is confirmed that there are no issue one can merge  by
```
git checkout main
git merge --no-ff radham0wn1ka-main
git push origin main
```
---
layout: post
title: Git backup site
---

A shell backup site by Git.<!-- more -->

    #!/usr/bin/env bash
    cd /var/www/demo
    mysqldump -u user -p password database > database.sql
    git add *
    git commit -am "$(date)"
    git push origin master
    git rm database.sql

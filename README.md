<!--
 * Licensed to the Apache Software Foundation (ASF) under one
 * or more contributor license agreements.  See the NOTICE file
 * distributed with this work for additional information
 * regarding copyright ownership.  The ASF licenses this file
 * to you under the Apache License, Version 2.0 (the
 * "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 -->
# Apache YuniKorn website

This readme will walk you through building the Apache YuniKorn website

## Introduction

1. The `master` branch contains the website source code. Every time you modify the website, you need to submit it to the `master` branch for saving.

2. The `asf-site` branch contains the deployed static pages, scripts and images of the website. Every time you modify the website, you need to save the latest generated static page set here.
 
https://yunikorn.apache.org will be updated automatically via the configuration set in the `.asf.yaml` file.

## Build website by docker

```
git clone https://github.com/apache/incubator-yunikorn-site.git
git checkout master

docker build -t yunikorn/yunikorn-website:1.0.0 .

docker run -it -p 4000:4000 -v $PWD/yunikorn-site:/yunikorn-site yunikorn/yunikorn-website:1.0.0 bash
cd /incubator-yunikorn-site
bundle exec jekyll serve --destination /yunikorn-site/ --watch --host=0.0.0.0
```

The static page of the website will be generated inside the docker image in the `/yunikorn-site` directory.
This directory will be located at `/yunikorn-site` on the host operating system, at the top-level of the source code tree.

You can view the new website locally on: http://localhost:4000/

## Deploy website

All these instructions expect that the current directory is the top-level directory of the repository.

1. Commit the `master` branch to GitHub repo.
1. Copy the `yunikorn-site` directory to a backup path **outside** the source tree, e.g. `mkdir ../backup-site && cp -R yunikorn-site/* ../backup-site`.
1. Checkout the `asf-site` branch, clear all the contents of the directory, e.g. `rm -rf ./*` (this leaves the files starting with a dot do not remove them!)
1. Copy the contents of the `backup-site` directory back to the top-level directory of the repo, e.g. `cp -R ../backup-site/* .`
1. Commit the `asf-site` branch to GitHub repo.

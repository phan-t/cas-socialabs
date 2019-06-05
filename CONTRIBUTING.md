This repository leverages Jekyll to build a static site at https://cas-socialabls.vmwapj.com

Refer to https://jekyllrb.com/docs/installation/ to install Jekyll on your local machine.

The text below (including the ---) can be used as a template for a new post.

---
title: Contributing # please don't embed a lesson number in the title. This will prevent flexibility of the content order at a later date
author: Grant Orchard
layout: cas # the Jekyll layout html that will be used for the post
date: 2019-05-15 # this metadata orders the posts in the series table
series: cas-socialabs  # this parameter collects the posts into a series and adds them to the 'series' table at the bottom of the post
permalink: /descriptive-permalink-separated-by-dashes/ # please don't embed a lesson number in the title. This will prevent flexibility of the content order at a later date. Make sure to keep the trailing slash.
description: 'This is an example markdown file that can be used to create a new module.'
image: /assets/images/example.png
---
We ask that you follow the provided headings for consistency between modules.

### Lab Objective
Describe what the purpose of the lab exercise is.

### Instructions
1. Use a numbered list to provide **guidance** but not step by step instructions.
2. We want people to feel a sense of accomplishment at figuring out how to do things within the platform.
3. If you think it will help, you can embed a gif or youtube video with the following syntax to take advantage of the lightbox. {% lightbox /assets/images/03.png --title="Start the lab" --alt="Using Cloud Assembly Blueprints" --data="getting-started" --img-style="max-width:80%" %}

### Hints
In this section you can provide examples, hints, or links that will assist people who might be struggling to progress.
You can use ```three backticks``` to provide code block formatting, or create a gist with {% gist gist_id %}.

### Solution
Create an [alternate page](https://with-a-link)containing requisite YAML or code snippets in the event that people get stuck. This is an optional section that may not apply to all lessons.

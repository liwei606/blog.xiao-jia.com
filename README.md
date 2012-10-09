markpress
=========

markpress is a very simple blogging script written in bash.

basic structure
---------------
```
.
├── _config.yml
├── _pages
│   └── about.md
├── _posts
│   └── 2012-12-21-hello-world.md
├── _template.html
├── CNAME
├── markpress*
└── style.css
```

`_config.yml`
-------------
This is the configuration file written in YAML. 
You are required to define 4 variables as follows.
```yaml
url: http://yourname.github.com/yourblog
title: Your Blog Title
author: Your Name
disqus: your_disqus_id
```
If you have a top-level domain for your blog, set `url` to `http://your-blog-host.com` or `http://blog.your-host.com`.

`_pages`
--------
You can put something like "About Me" in this directory. 
There will be links to the pages in the navigation menu on every page.

Pages are required to be written in Markdown format, with a YAML front matter:
```markdown
title: About Me

Hi, this is me!
```
markpress reads the page content starting from the third line of a page file. 
So remember to add a blank line between the YAML front matter and your Markdown text.

`_posts`
--------
This is where you put your blog posts. Sample YAML front matter:
```yaml
title: Hello World
tags: tag1, tag2
date: 2012-12-21 12:34:56
```
You can also use `tag` and `time` instead of `tags` and `date`, respectively.

`_template.html` and `style.css`
--------------------------------
These two files together are the Twenty Twelve theme for Wordpress.
I tweaked them a little to suit my own taste. So feel free to change them.

`CNAME`
-------
If you want use your own domain for your blog, put your domain in this file (e.g. `blog.xiao-jia.com`).

`markpress`
-----------
After you prepared all the stuffs above, run `./markpress` from a bash shell, and 
all your site contents will be generated automatically.

Work with GitHub Pages
----------------------
markpress is designed to work with GitHub Pages. 
You can push these files (including generated ones) to either `master` or `gh-pages` branch. 
Remember to keep both your markdown files and the generated files in the same branch 
(this is *different* from Jekyll and Octopress)! 
Maintaining two not-much-related branches for blogging is just annoying.

License
-------
```
            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE 
                    Version 2, December 2004 

 Copyright (C) 2004 Sam Hocevar <sam@hocevar.net> 

 Everyone is permitted to copy and distribute verbatim or modified 
 copies of this license document, and changing it is allowed as long 
 as the name is changed. 

            DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE 
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION 

  0. You just DO WHAT THE FUCK YOU WANT TO. 
```

---
layout: post
title:  Setting up a free website using Jekyll and GitHub pages
date:   2014-12-20 22:18:00
---
Recently I was able to cut down on some of my site hosting costs by moving to [GitHub Pages](https://pages.github.com/),
a free way to host public websites of static content. It won't work for something like WordPress where you need to run
something server side, but it works great for plain .HTML pages for instance. Also, by using
[Jekyll](http://jekyllrb.com/) you can dynamically generate static .HTML pages for your site, allowing you to do some
cool stuff like generate blog posts from [easy-to-write markdown](http://daringfireball.net/projects/markdown/syntax)
files.

[Here's how you can get started with your own GitHub site](https://help.github.com/articles/using-jekyll-with-pages/),
summarized below:

1. Install [the latest version of ruby](https://www.ruby-lang.org/en/downloads/).
2. Open the command prompt and run `gem install bundler` to install Bundler, a ruby package manager.
3. Save [this file](https://gist.github.com/ChristianWilkie/5b54228e5a101a3a793b#file-gemfile) as "Gemfile"
(no file extension) in the folder where you want to build your GitHub site (note: if the gist link doesn't work, check
[here](https://help.github.com/articles/using-jekyll-with-pages/#installing-jekyll) for instructions on making that
 file.
4. Open a command prompt from within the folder for the previous step and type `bundle install`. This should install
Jekyll and any needed dependencies.
5. Execute `bundle exec jekyll new . --force` into the command prompt inside your site folder. This will create a simple
base template to build your site off of.
6. Lastly, execute `bundle exec jekyll serve` into the same command prompt and your site should be dynamically
generated and available for viewing at `http://localhost:4000`.

Now, whenever you want to start working on your site, just start Jekyll by typing `bundle exec jekyll serve` and then
begin editing! By default Jekyll will watch your site folder for changes and automatically recreate site content as you
save your files.

To upload your site to GitHub, do the following (summarized below):

1. [Create a new repository](https://github.com/new) called `username.github.io`, where `username` is replaced by your
GitHub username.
2. Init a new Git repository by typing `git init .` in a command window in your site's root directory.
3. Type `git remote add origin git@github.com:username/username.github.io.git`, replacing `username` with your GitHub
username as needed.
4. Type `git push -u origin master` to push your site to GitHub

Your site should then appear on GitHub at `http://username.github.io` after a short time (maybe 10-15 minutes for it
to be generated for the first time).

To learn more about using Jekyll itself, check out the [official Jekyll site](http://jekyllrb.com/), and especially the
 subpage on [writing posts](http://jekyllrb.com/docs/posts/).
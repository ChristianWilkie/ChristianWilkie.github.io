# ChristianWilkie.github.io

Main URL: http://www.christianwilkie.com/


### Quick Initial Setup on Ubuntu 20.10
1. `sudo apt-get install ruby-full build-essential`
2. `sudo gem install bundler`
3. `sudo bundle update --bundler`
4. `bundle update`
5. start the site with `bundle exec jekyll serve`
6. check it out at http://localhost:4000/

See: also https://jekyllrb.com/docs/

## Making a new post (new way)

1. Go to [https://prose.io/#ChristianWilkie/ChristianWilkie.github.io/new/master/_posts](https://prose.io/#ChristianWilkie/ChristianWilkie.github.io/new/master/_posts)
2. Use the WYSIWYG editor - remember to change the title

## Making a new post (old way)

1. run `bundle exec jekyll post "Raspberry Pi - Test SD Card Speed"`

for more info: https://github.com/jekyll/jekyll-compose

## troubleshooting

### error with EventMachine C extension
Example: `Unable to load the EventMachine C extension; To use the pure-ruby reactor, require 'em/pure_ruby'`

Solution:
1. run `gem uninstall eventmachine`
2. run `gem install eventmachine --platform ruby`

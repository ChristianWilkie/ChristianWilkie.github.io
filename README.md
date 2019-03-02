# ChristianWilkie.github.io

Main URL: http://www.christianwilkie.com/


## Installing a local dev environment

See: https://jekyllrb.com/docs/

Summary:
1. Install ruby+devkit
2. run `gem install jekyll bundler` to install jekyll/bundler
3. run `bundle update` to update gems
4. start the site with `bundle exec jekyll serve`

## troubleshooting

### error with EventMachine C extension
Example: `Unable to load the EventMachine C extension; To use the pure-ruby reactor, require 'em/pure_ruby'`

Solution:
1. run `gem uninstall eventmachine`
2. run `gem install eventmachine --platform ruby`
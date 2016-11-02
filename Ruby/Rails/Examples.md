# Rails Examples to Learn From

* [Recurring Events in Rails](http://nithinbekal.com/posts/rails-recurring-events/)

```ruby
remotes.sort.last
remotes.max

options.keys.include?(:page)
options.key?(:page)

File.open(fname, 'w') do |f|
  f.write(content)
end
File.write(fname, content)

Post.where(user_id: user.id)
user.posts

RUBY_PLATFORM =~ /java/
/java/.match?(RUBY_PLATFORM)
RUBY_PLATFORM.include?('java')

require File.expand_path('../boot', __FILE__)
require File.expand_path('boot', __dir__)
require_relative 'boot'

User.new(name: args[:name], email: args[:email])
User.new(args.slice(:name, :email))

options = super
options[:secure] = true
options
super.tap do |options|
  options[:secure] = true
end

Logger.new(STDOUT) # Don't use constant, use variable
Logger.new($stdout)

/\A \z/
```

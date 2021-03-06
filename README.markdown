# parallelize

Simple multi-threading for Ruby.

## Installation
```
gem install parallelize
```

## Examples
```ruby
require 'rubygems'
require 'parallelize'

parallelize(4) do
  puts "I'm a thread"

  # ...
end

# Zero-based thread index
parallelize(4) do |thread_idx|
  puts "I'm thread ##{thread_idx}"

  # ...
end

# Enumerable#peach
(0..100).peach(4) do |elem, thread_idx|
  puts "Thread ##{thread_idx} processing #{elem}"
end

# Enumerable#pmap
(0..100).pmap(4) do |elem|
  elem ** 2
end

(0..100).pmap(8) do |elem, thread_idx|
  elem * thread_idx
end
```

### Collecting exceptions
```ruby
begin
  parallelize(4, true) do |elem, thread_idx|
    # Each thread can complete its block even when some other threads throw exceptions
  end
rescue ParallelException => e
  p e.exceptions
end
```

## Contributing to parallelize
* Check out the latest master to make sure the feature hasn't been implemented or the bug hasn't been fixed yet
* Check out the issue tracker to make sure someone already hasn't requested it and/or contributed it
* Fork the project
* Start a feature/bugfix branch
* Commit and push until you are happy with your contribution
* Make sure to add tests for it. This is important so I don't break it in a future version unintentionally.
* Please try not to mess with the Rakefile, version, or history. If you want to have your own version, or is otherwise necessary, that is fine, but please isolate to its own commit so I can cherry-pick around it.

## Copyright

Copyright (c) 2011 Junegunn Choi. See LICENSE.txt for
further details.


# Logging

The `logger` is automatically mixed into all driver classes and has the usual logger levels:

* `debug`: use debug often for verbose output - not saved to log files by default
* `info`: anything you are interested in seeing in the log file
* `warn`: something might be wrong, possibly worth investigation.
* `error`: something went wrong, definitely worth investigation
* `fatal`: something that should never go wrong, went wrong. Requires immediate investigation / resolution

If text being passed to the logger requires some string manipulation or other processor intensive operation, it is worth performing this work in a [block](http://www.eriktrautman.com/posts/ruby-explained-blocks-procs-and-lambdas-aka-closures) in case the result is not recorded - this is preferred with debug statements as they are discarded when nobody is watching.

```ruby
def received(data, resolve, command)
    logger.debug {
        cmd = String.new("Device sent 0x#{byte_to_hex(data)}")
        cmd << " for command #{command[:name]}" if command
        cmd # return the text to be displayed if we are debugging
    }
end
```

There is also a handy helper method for formatting errors:

```ruby
begin
    raise 'whoa!'
rescue => e
    logger.print_error e, 'optional additional description of error'
end
```


# Scheduling Actions

Every driver can schedule events to occur in a number of different ways. Schedules are automatically cleared when a driver is terminated.

* Integer arguments are in milliseconds. `1000` == 1 second
* Strings can be used for a friendly representation of the time
  * `'30s'` == 30 seconds
  * `'5m'` == 5 minutes
  * `'1w2d3h5m'` == 1 week, 2 days, 3 hours and 5 minutes
  * `'2Y1M'` == 2 years, 1 month

| Function | Arguments | Description |
| :--- | :--- | :--- |
| `schedule.in` | String or Integer | schedule a task to run once in the time specified \(formats above\) |
| `schedule.at` | Time or String | schedule a task at a time represented by a [Time object](http://ruby-doc.org/core-2.5.0/Time.html) or a parsable [time string](http://ruby-doc.org/stdlib-2.5.0/libdoc/date/rdoc/DateTime.html#parse-method) |
| `schedule.every` | String or Integer | schedule a task to run every time period on repeat |
| `schedule.cron` | String | A schedule that will fire based on a [CRON](https://en.wikipedia.org/wiki/Cron) string |
| `schedule.clear` |  | shortcut for cancelling any active schedules |

## Examples

```ruby
schedule.every('1m') do
    # perform some action, such as polling
end

schedule.in(500) do
    # ...
end

schedule.at(Time.now + 2.hours) do
    # ...
end

schedule.at('2018-02-02T15:32:41+11:00') do
    # ...
end

# Every day at 8am
schedule.cron('0 8 * * *') do
    # ...
end

# Canceling an individual schedule
@email_sched = schedule.in(500) do
    send_email
end
@email_sched.cancel
```

There are often situations where you want to run the block immediately.

```ruby
def connected
    schedule.every('1m', :run_now) do
        poll_current_state
    end
end
```

CRON also supports time zones - which should always be configured

```ruby
schedule.cron('0 8 * * *', timezone: 'Sydney') do
    # ...
end
```

See the list of supported [time zone strings](http://api.rubyonrails.org/classes/ActiveSupport/TimeZone.html) and information [about time zones](https://robots.thoughtbot.com/its-about-time-zones).


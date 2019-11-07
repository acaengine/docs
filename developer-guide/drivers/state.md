# State

A driver should be built to represent the state of the device or service it is abstracting.

* User interfaces can bind to state to provide visual feedback
* Logic can query state and subscribe to state changes to trigger further actions

{% hint style="danger" %}
Driver state is should always be considered public and as such, should never contain any sensitive information \(auth details, access tokens etc\).
{% endhint %}

* Any authenticated user can read the state
* Do not store sensitive material in state

## Exposing State

A driver [quacks](https://en.wikipedia.org/wiki/Duck_typing) like a hash

{% hint style="info" %}
All state keys must be [Symbols](https://ruby-doc.org/core-2.4.2/Symbol.html), [Strings](https://ruby-doc.org/core-2.4.2/String.html) or respond to `#to_sym`
{% endhint %}

* Setting state `self[:state_key] = 'value'`
* Reading state `self[:stafe_key] # => 'value'`

Logic can access driver state in the same way

* Reading state `system[:Display][:power] # => true`
* Setting state `system[:Display][:not_recommended] = true`

Logic might trigger a useful action by changing the state of other drivers directly, however generally it is recommended to use a [mutator method](https://en.wikipedia.org/wiki/Mutator_method).

{% hint style="success" %}
All state values should be limited to objects that can be converted to JSON for transmitting over the API.
{% endhint %}

* JSON compatible classes: `nil, true, false, Hash, String, Integer, Array, Float, Symbol`
* Objects that respond to: `#to_json` or failing that `#to_s` will be called when sending over the API
* Objects that don’t meet these requirements can be used server side and are sent as `nil` over the API

## Subscribing to State

All drivers can subscribe to their own state.

```ruby
# Subscribe to internal stateref = subscribe(:state_variable) do |notify|    notification.value     # => value of the status variable that triggered this notification    notification.old_value # => the value of the variable before this change    # Also comes with the subscription information    notify.sys_name # => The system name    notify.sys_id   # => The system ID this value originated from    notify.mod_name # => The generic module name     notify.mod_id   # => The module database ID    notify.index    # => The device index    notify.status   # => the name of the status variable    # And a reference to the subscription should you want to unsubscribe    unsubscribe(notification.subscription)end# Optionally unsubscribeunsubscribe(ref)
```

Logic can additionally subscribe to state of other drivers.

## Change detection

When state is applied it is checked against the existing value and subscribers are only notified if the value has changed.

```ruby
self[:power] = On  # => subscribers are notified of the changeself[:power] = On  # => no change detected, no action takenself[:power] = Off # => subscribers are notified of the change
```

Change detection doesn’t work if you mutate a variable.

```ruby
self[:my_array] = [1, 2, 3] # => subscribers are notified of the changeself[:my_array] << 4        # => no action taken (change detection isn't run)@my_copy = self[:my_array]@my_copy << 5self[:my_array] = @my_copy  # => no change detected (change detection did run)# Only if you are really sure you know what you are doing!signal_status(:my_array)    # => forces a change notification to subscribers
```

{% hint style="warning" %}
Mutating complex status variables is **not recommended** as the variables might be being acted upon on another thread. This can lead to race conditions or worse.
{% endhint %}

The recommended method for updating complex state is:

1. **Duplicate** `my_array = ['my', 'array'].dup` or `{complex:['hash']}.deep_dup`
   * `.deep_dup` when in doubt
2. **Update** `my_array << 8`
3. **Apply** `self[:my_array] = my_array`

This can be achieved by using operations that create a new object

```ruby
self[:my_array] = [1, 2, 3] # => subscribers are notified of the changeself[:my_array] += [4]      # => subscribers are notified of the changeself[:my_array]             # => [1, 2, 3, 4]# These will both trigger notificationsself[:my_hash] = { example: 1 }self[:my_hash] = self[:my_hash].merge({ update: true })self[:my_hash] # => { example: 1, update: true }
```


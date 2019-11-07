# Security

Authentication is mandatory and authenticated users have access to all systems and drivers within. They can’t edit or see settings, can’t list systems or change anything however they can, by default, access all functions defined in drivers if they know the system id. This is via the websocket API, most restful API’s are out of bounds to a regular user.

A global callback can be defined to check if a user should be able to access a system:

In a [Rails initialiser](http://guides.rubyonrails.org/configuring.html#using-initializer-files):

```ruby
# Returning true means access should be grantedRails.application.config.orchestrator.check_access = proc { |system_id, user|    if system_id == 'sys-nuclear-warheads'        user.sys_admin ? true : false    else        # We only want to block access to the warheads        true    end}
```

All drivers have a helper method for accessing the user details so you can manually manage permissions:

```ruby
def some_method_in_driver    user = current_user    if user.nil?        # Method was invoked internally - timer, onload callback etc    else        logger.info "Method called by user #{user.email} (#{user.id})"    endend
```

You can also protect methods using `protect_method`. The last `protect_method` call for any function is the one that will be used.

```ruby
class Some::Device::Driver    include ::Orchestrator::Security    # By default both Tech Support and Admin users have access to these methods    # Regular users will be rejected    protect_method :method_1, :method_2    # if you provide a block then it can be used to decide if a user should have access    protect_method :method_1, :method_2 do |user|        user.sys_admin || user.name == 'service account' || check_room_bookings(user)    end    def method_1; end    def method_2; endend
```

you can also check if a user has access to a method

```ruby
can_access? :method_name# by default it checks against the current user, this can be overriddencan_access? :method_name, user
```

NOTE:: the current user is maintained across asynchronous function calls and timers.

i.e. `Browser (user: Bob) -> LogicModule.do_something_weird -> Display.reset_to_factory_new`

If Bob is a regular user and the `reset_to_factory_new` function is protected then `reset_to_factory_new` will not be executed.

Finally all system access is logged and saved for a few months to make it fairly easy to track down bad actors within an organisation.

## Encrypted Settings

Passwords often need to be stored in the database for accessing secure devices. To have a setting stored securely, you enter the key with a `$` sign prefix.

```javascript
{    "$password": "secret"}
```

once saved, the setting is encrypted with 256 bit [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) using [GCM](https://en.wikipedia.org/wiki/Galois/Counter_Mode) ciphers to prevent tampering

You can review the code here: [https://github.com/acaprojects/ruby-engine/blob/master/lib/orchestrator/encryption.rb](https://github.com/acaprojects/ruby-engine/blob/master/lib/orchestrator/encryption.rb)


# Development Environment

Engine is distributed as a set of docker containers that are designed to deploy to your on-prem infrastructure or private cloud. To keep things simple for development, testing, and experimentation this is also packaged as a prebuilt environment that you can run on your local machine.

This environment runs across MacOS, Windows, or Linux - feel free to pick where you work best.

## Required Tooling

In order to run this environment you will need two common tools:

1. [ ] [Vagrant](https://www.vagrantup.com/downloads.html): a tool for managing virtual environments.
2. [ ] [VirtualBox](https://www.virtualbox.org/wiki/Downloads): an open source, cross-platform virtualisation provider.

Outside of these, nothing will need to be installed or modified on your machine.

Setup these now, then drop back - we’ve prepared some music to play while you do this...

{% embed url="https://youtu.be/S5PvBzDlZGs" %}

Welcome back.

## Building Your Environment

Now that you have the required tools, choose a directory where you'd like to work, then run

```bash
vagrant init acaengine/dev-env
```

This will create a [Vagrantfile](https://www.vagrantup.com/docs/vagrantfile/) that contains your environment config.

{% hint style="success" %}
If you are planning on diving into [driver development](drivers/), you can also fork and clone the [open-source drivers repo](https://github.com/acaprojects/ruby-engine-drivers/), which contains a pre-initialised Vagrantfile ready for use.
{% endhint %}

{% hint style="warning" %}
Older versions of the development environment used the `vagrant-triggers` plugin. This is no longer needed, or compatible with modern versions of Vagrant. If you see a warning about this, run:`vagrant plugin uninstall vagrant-triggers`before continuing.
{% endhint %}

### Starting Up

Open a terminal window in the same directory as your vagrant file and run:

```bash
vagrant up
```

You will see some updates while your environment boots up. This may take a couple of minutes the first time it runs. When it’s complete you will be provided with a URL and authentication details to log in.

Congratulations you’re ready to go!

{% hint style="info" %}
Vagrant commands need to run within the folder containing the environment configuration \(i.e. where your Vagrantfile is\).

If you get an error that says: `A Vagrant environment or target machine is required to run this command` check that you’re in the right place.
{% endhint %}

### Shutting Down

When you’re done working with Engine use

```bash
vagrant halt
```

to shutdown your environment.

You can continue to use these two commands to start and stop your local Engine instance as you need.

### Starting Over

Changes that you make, such as adding or removing devices, systems, or zones will persist across restarts. To return to a fresh deployment run

```bash
vagrant destroy
```

The next time you run `vagrant up` you'll be presented with a fresh deploy.


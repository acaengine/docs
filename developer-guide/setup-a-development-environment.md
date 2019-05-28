# Setup a Development Environment

The ACA Engine development environment runs on MacOS, Windows, or Linux – feel free to pick where you work best.

This environment contains virtualised infrastructure and reflects what you will use within a production deployment. To run this, you will need a few common tools:

1. [Vagrant](https://www.vagrantup.com/downloads.html): a tool for managing virtual environments.
2. [VirtualBox](https://www.virtualbox.org/wiki/Downloads): an open source, cross-platform virtualisation provider.
3. [Git](https://git-scm.com/): distributed version control software.

Outside of these, nothing will need to be installed or modified on your machine.

Setup these tools now, then drop back. We’ve prepared some music to play while you do this.

{% embed url="https://youtu.be/S5PvBzDlZGs" %}

Welcome back.

Now that you have the required tools, [download or clone the ACA Engine development environment](https://github.com/acaprojects/setup-dev). This will tell Vagrant how to create and deploy your environment.

Open a terminal in the containing folder and run:

```bash
vagrant up
```

You will see some updates while your environment provisions. This may take a couple of minutes the first time it runs. When it’s complete you will be provided with a URL and authentication details to log in. Congratulations you’re ready to go!

When you’re done working with ACA Engine use

```bash
vagrant halt
```

to shutdown your environment.

{% hint style="info" %}
Vagrant commands need to run within the folder containing the environment configuration \(i.e. where you saved the `setup-dev` repository\).

If you get an error that says: `A Vagrant environment or target machine is required to run this command` check that you’re in the right place.
{% endhint %}

You can continue to use these two commands to start and stop your local ACAEngine instance as you need.

Changes that you make, such as adding or removing devices, systems, or zones will persist across restarts. To return to a fresh deployment run:

```bash
vagrant destroy
```

The `setup-dev` directory contains the entire development environment. You can move this between machines by copying it. Similarly, to completely remove it from your machine, delete it.


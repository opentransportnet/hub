# The Open Transport Net Hub installation repository

Set up an Open Transport Net (OTN) Hub for your city using vagrant

## How to

### First time
 * install vagrant: https://www.vagrantup.com/
 * Add the ip addresses in the hosts file to your `/etc/hosts file (see Vagrantfile)
 * $`vagrant up`

### Update

 * git pull
 * vagrant provision

### Install in production

_todo_ - See deliverables

## Multi-Machine set-up ##

See https://docs.vagrantup.com/v2/multi-machine/

We are setting up different virtual machines per tool.
 * The DataTank has the http://tdt.hub.dev machine
 * We have a separate machine for the databases right now. We have mysql running on IP address 192.168.70.71
 * ... todo

## Git workflow ##

### You're one of the main contributors ###

We follow the git branching model. This means that there should be only 4 commits on `master` after bootstrapping the repository: service level 1, service level 2, 3 and 4. All of these commits are translated into `tags` or github `releases`. Right now, they are milestones.

_How to commit?_ Everyone starts off the `development` branch. Also on this branch we will not push directly. We will branch this into our `feature-{featurename}` branch. Over there we can add our changes. When having pushed this branch on the github repository, and you have tested any possible regression, you can now perform a pull request to pull your changes into the development branch.

### You don't have access to the main fork ###

You just fork it, and do a pull request to our development branch :)

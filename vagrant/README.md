# Vagrant

## Prerequisites

Please install the following:

- [VirtualBox](https://www.virtualbox.org/)
- [Vagrant](https://www.vagrantup.com/)
- [vagrant-disksize](https://github.com/sprotheroe/vagrant-disksize) plugin

### MacOS

```bash
brew cask install virtualbox
brew cask install vagrant
vagrant plugin install vagrant-disksize
```

## Setting up

You can set up the Vagrant environment with just one command:

```bash
vagrant up
```

After successfull installation you can ssh to the virtual machine with:

```bash
vagrant ssh
```

### Troubleshooting

If you see error similar to the following during `vagrant up`:

```bash
default: + sudo -H -u vagrant -i helm2 init --wait
default: Creating /home/vagrant/.helm
...
default: Adding stable repo with URL: https://kubernetes-charts.storage.googleapis.com
default: Adding local repo with URL: http://127.0.0.1:8879/charts
default: $HELM_HOME has been configured at /home/vagrant/.helm.
default: Error: error installing: Post "http://localhost:8080/apis/apps/v1/namespaces/kube-system/deployments": dial tcp 127.0.0.1:8080: connect: connection refused
```

then after ssh-ing into the machine, re-run the command:

```bash
helm2 init --wait
```

and then run `helm2 version` to make sure everything is OK.

## Build

To perform docker image build and to run tests please use `build` target:

```bash
/sumologic/vagrant/Makefile build
```

## Collector

To install or upgrade collector please type:

```bash
/sumologic/vagrant/Makefile upgrade
```

This command will prepare environment (namespaces, receiver-mock, etc.)
and after that it will install/upgrade collector in the vagrant environment.

To remove collector please use:

```bash
/sumologic/vagrant/Makefile clean
```

List of other useful commands in the Makefile:

- `expose-prometheus` - exposes prometheus on port 9090 of virtual machine
- `expose-grafana` - exposes grafana on port 8080 of virtual machine
- `apply-avalanche` - run one pod deployment of avalanche (metrics generator)

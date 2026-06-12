This builds a Vagrant Fedora Bluefin Base Box.

Currently this targets [Fedora Bluefin (DX)](https://projectbluefin.io/) 44 (which is based on [Fedora Silverblue](https://silverblue.fedoraproject.org/)).


# Usage

Install [Packer](https://www.packer.io/) and [Vagrant](https://www.vagrantup.com/).

## qemu-kvm usage

Install qemu-kvm:

```bash
apt-get install -y qemu-kvm
apt-get install -y sysfsutils
systool -m kvm_intel -v
```

Type `make build-libvirt` and follow the instructions.

Try the example guest:

```bash
cd example
apt-get install -y virt-manager libvirt-dev
vagrant plugin install vagrant-libvirt
vagrant up --provider=libvirt
vagrant ssh
exit
vagrant destroy -f
```


# Kickstart

The Fedora installation iso uses the Anaconda installer to install Fedora.
During the installation it will ask you some questions and it will also
store your answers in the `/root/anaconda-ks.cfg` (aka kickstart) file.
This file is later used to fully automate a new installation by specifying
its location in the `inst.ks` kernel command line argument.


# Reference

* [Anaconda boot options](https://anaconda-installer.readthedocs.io/en/latest/boot-options.html)
* [Kickstart manual](http://pykickstart.readthedocs.io/en/latest/kickstart-docs.html)
* [Kickstart Syntax Reference](https://anaconda-installer.readthedocs.io/en/latest/kickstart.html)
* [Project Bluefin](https://projectbluefin.io)
  * [Bluefin Installation](https://docs.projectbluefin.io/installation/)
  * [Bluefin source-code repository](https://github.com/ublue-os/bluefin)
  * [Bluefin Images](https://docs.projectbluefin.io/images/)
    * Show a image manifest:
      ```bash
      oras manifest fetch ghcr.io/ublue-os/bluefin-dx:44 --platform linux/amd64 | jq
      regctl manifest get ghcr.io/ublue-os/bluefin-dx:44 --platform local
      ```
  * [Bluefin image packages list](https://github.com/orgs/ublue-os/packages?repo_name=bluefin)
  * [Bluefin image packages](https://github.com/ublue-os/bluefin/pkgs/container/bluefin)
* [`bootc` Documentation](https://docs.fedoraproject.org/en-US/bootc/)
  * [Getting Started Guide](https://docs.fedoraproject.org/en-US/bootc/getting-started/)
  * [Installing on Bare Metal](https://docs.fedoraproject.org/en-US/bootc/bare-metal/)
  * [Base Images](https://docs.fedoraproject.org/en-US/bootc/base-images/)
  * [Base Images source-code repositories](https://gitlab.com/fedora/bootc/base-images)

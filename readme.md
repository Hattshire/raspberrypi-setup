# Raspberry Pi Setup/Scripts/Güereber'llu'colit

Some fancy things to setup my rpi, so if I fk'up the MicroSD I can get it back running without doing the boring stuff again.

I'm using it as a local server, as this is the only easy to get not-that-expensive low-power thing I can use for now.

## Getting Started

### Prerequisites and/or asumptions

* The rpi is already connected to lan (wifi or eth, doesn't matter, for now).
* The rpi has Raspbian/RaspberryPi OS Lite (x32) installed
* The rpi names itself `raspberrypi`, and thus it's network address is `raspberrypi.local`
  * If not, edit `ansible/hosts.yml`. More info [>here<](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#hosts-in-multiple-groups).
* The local computer has python 3 with pycrypto and ansible installed
* SSH was configured to log in with a [private key](https://www.ssh.com/ssh/copy-id#copy-the-key-to-a-server), on pi user (`ssh r..pi.local` is sufficent to be in), and pi user's [password is no longer "raspberry"](https://www.shellhacks.com/raspberry-pi-default-password-how-to-change/) (Security first, even if my ISP doesn't give me any open ports to the Public :c)

### Specs/limitations (at the time of writting)
```
Board:
  - Raspberry PI 4
  - Model B
  - 2GB RAM

MicroSD: 
  - Sandisk 4GB class 4

Power:
  - 2A usb charger (that probably doesn't deliver more than 1A, but idk)

Peripheals:
  - No Display
  - No Sound
  - No Case
  - No nothing
  ...
  - Kingston 16GB USB Stick for local storage (as I can't power the hdd I have externally for now)

```

### Ansible Roles

Everything I did has an ansible role, so I can remake an identical system, they are:

* _dns_: DNS service with _dnsmasq_
* _http_: Simple LAMP Stack setup
* _RabbitMQ_: Message Broker
* _transmission_: Transmission Torrent Daemon accesible from LAN
* _turtl_: Personal Turtl service
* _usbmount_: Automount USB drives, correctly
* _zenko-cloudserver_: S3-compatible ObjectStorage service with multicloud agregation support

> UPNEXT: miniDLNA - mpd

### System Preparation

> TODO Set wifi settings before step 2

 1. Install Raspberry Pi OS Lite x32 via "Raspi Card Imager" Android app with the "Headless" and "Enable ssh" options selected on a clean microsd card.
 
 2. Install the msd on the pi
 
 3. Connect the pi to the network with eth. and power on.
 
 3.1. (optional) Connect to wifi editing `/etc/wpa_supplicant/wpa_supplicant.conf` using ssh
 
 4. Update the system

### Setup


 1. First, set a vault password creating the vault password file on the local home dir

 ```
 echo P45UWURD > ~/.ansible_rpi_vault
 ```

 2. Recreate the vault
 > Note: variables to set are specified in the group_vars/rpi/vars file (not so clearly but at least not shady)

 ```
 cd ansible
 ansible-vault create group_vars/rpi/vault
 ```
 
 3. Install dependencies
 
 ```
 cd ansible
 ansible-galaxy install -r requirements.yml
 ```

 4. Finally, run the main playbook

 ```
 cd ansible
 ansible-playbook site.yml
 ```

_As of 03NOV2020 every playbook works as intended._

## Built With

* [Ansible](https://docs.ansible.com/) - That thing to automate things on other things that aren't the local thing but it can also be used there.
* [luv <3](https://uwu.email/) - UwU



## Authors

* **Me** - *Puked this repo* - [Hattshire@Github](https://github.com/Hattshire)

## License

This project is (un)licensed under the UNLicense - see the [UNLICENSE.md](UNLICENSE.md) file for details

## Acknowledgments

* [Artemmkin/Infrastructure As Code Tutorial](https://github.com/Artemmkin/infrastructure-as-code-tutorial) for kickstarting me to the ansible side of things
* [Pi My Life Up](https://pimylifeup.com/) for simplifying the dns setup for me
* Loose screws on my linux setups
* My cat _Teo_ for beign so cute <3 But at the same time so traitor with my feelings :'c

## Side Notes
Yes this was a template, a very good one, so good U want to use it too, here here:

[PurpleBooth/README-Template.md](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)

I know you want it 7u7

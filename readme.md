# Raspberry Pi Setup/Scripts/Güereber'llu'colit

Some fancy things to setup my rpi, so if I fk'up the MicroSD I can get it back running without doing the boring stuff again.

I'm using it as a local server, as this is the only easy to get not-that-expensive low-power thing I can use for now.
(It costs a rough maximum of 1.6USD monthly to run at full usage 24/7, almost any other cheap linux-ready thing would cost me more than 10USD monthly to run not even at idle, and I have no money source currently, and energy here is kinda expensive, and Google is still evil, and internet things doesn't automate over magic)

## Getting Started

### Prerequisites and/or asumptions

* The rpi is already connected to lan (wifi or eth, doesn't matter, for now).
* The rpi has Raspbian/RaspberryPiOS Lite installed
* The rpi names itself `raspberrypi`, and thus it's network address is `raspberrypi.local`
* The local computer has python 3 with pycrypto and ansible installed
* SSH was configured to log in with a private key, on pi user (`ssh r..pi.local` is sufficent to be in), and pi user's password is no longer "raspberry" (Security first, even if my ISP doesn't give me any open ports to the Public :c)

#### Specs/limitations (at the time of writting)
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

#### Playbooks

Everything I did has an ansible playbook, so I can remake an identical system, they are:

* _dns.yml_: DNS service with _dnsmasq_
* _http.yml_: Simple LAMP Stack setup
* _transmission.yml_: Transmission Torrent Daemon accesible from LAN
* _turtl.yml_: Personal Turtl service
* _usbmount.yml_: Automount USB drives, correctly

> UPNEXT: miniDLNA - mpd - RabbitMQ

### Setup

> TODO DOCUMENT EARLY SETUP

First, set a vault password creating the vault password file on the local home dir

```
echo P45UWURD > ~/..ansible_rpi_vault
```

Recreate `http.vault.yml` and `turtl.vault.yml`
> Note: variables to set are specified in the respective playbook (not so clearly but at least not shady)

```
cd ansible
ansible-vault create http.vault.yml
ansible-vault create turtl.vault.yml
```

Run the playbooks one by one
> TODO UNIFY PLAYBOOKS

```
cd ansible
ansible-playbook usbmount.yml
ansible-playbook dns.yml
ansible-playbook http.yml
ansible-playbook transmission.yml
ansible-playbook turtl.yml
```

_As of 11JULY2020 every playbook works as intended._

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
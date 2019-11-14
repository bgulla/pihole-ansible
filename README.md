# PiHole Local-DNS Configuration with Ansible

## Local DNS Entries
Add an entry to the flat file `./roles/pihole/templates/localnet.list.j2` as specified below.
#### ./roles/pihole/templates/localnet.list.j2
```bash
#  _                 _           _
# | | ___   ___ __ _| |       __| |_ __  ___
# | |/ _ \ / __/ _` | |_____ / _` | '_ \/ __|
# | | (_) | (_| (_| | |_____| (_| | | | \__ \
# |_|\___/ \___\__,_|_|      \__,_|_| |_|___/
#
############################
# Format: 'IP	FQDN	SHORTHOSTNAME'
############################

10.0.5.7	larkspur.lol larkspur
10.0.5.11	k8smaster.lol	k8smaster
```

## Wildcard DNS
Add an entry to the flat file `./roles/pihole/templates/02-localnet.conf.j2` as specified below.
#### ./roles/pihole/templates/02-localnet.conf.j2
```bash
# Local network dnsmasq config
# {{ ansible_managed }}
addn-hosts=/etc/pihole/localnet.list
localise-queries
no-resolv

#           _ _     _                   _
# __      _(_) | __| | ___ __ _ _ __ __| |
# \ \ /\ / / | |/ _` |/ __/ _` | '__/ _` |
#  \ V  V /| | | (_| | (_| (_| | | | (_| |
#   \_/\_/ |_|_|\__,_|\___\__,_|_|  \__,_|
#
##################
# FORMAT: 'address=/DOMAIN/IP_OF_LOADBALANCER' -> *.domain.tld

# Local wildcard
address=/k8s.lol/10.0.5.44
```

## Running the playbook
```bash
ansible-playbook -i ./inventories/home/hosts pihole.yml
```

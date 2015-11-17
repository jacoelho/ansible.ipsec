jacoelho.ipsec
=========

An ansible role that installs and setup ipsec transport on Ubuntu.

Tested on ubuntu 14.04 (Trusty)

Only tested for ipsec transport between hosts.

Role Variables
--------------

The following variables are available:

    ipsec_psk: "password"
    ipsec_crypto_algorithm: "aes_256"
    ipsec_crypto_hash: "sha1"
    ipsec_crypto_authentication: "hmac_sha1"
    ipsec_dh_group: "modp1024"
    ipsec_pfs_group: "2"
    ipsec_lifetime: "time 12 hour"


Specify the IPs with secure communication:

    ipsec_hosts:
      - 1.1.1.1
      - 2.2.2.2
      - 3.3.3.3


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
        - { role: jacoelho.ipsec }

License
-------

BSD

Author Information
------------------

This role was created in 2015 by [José Coelho](https://github.com/jacoelho)

# Snappy LxdMosaic

**DONT USE - NOT READY FOR GENERAL USE**

Based on Nextcloud

Consists of:

- LxdMosaic
- Apache 2.4
- PHP 7.3
- MySQL 5.7

## How to install

[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-white.svg)](https://snapcraft.io/lxdMosaic)

There are a [number of releases available][1]. By default you'll get the newest
stable one, but you may be interested in others.


## How to use

After install, assuming you and the device on which it was installed are on the
same network, you should be able to reach the Nextcloud installation by visiting
`<hostname>.local` in your browser. If your hostname is `localhost` or
`localhost.localdomain`, like on an Ubuntu Core device, `nextcloud.local` will
be used instead.

Upon visiting the Nextcloud installation for the first time, you'll be prompted
for an admin username and password.

**The default username is admin and the password is test123**

#### HTTP/HTTPS port configuration

**UNTESTED**

By default, the snap will listen on port 80. If you enable HTTPS, it will listen
on both 80 and 443, and HTTP traffic will be redirected to HTTPS. But perhaps
you're putting the snap behind a proxy of some kind, in which case you probably
want to change those ports.

If you'd like to change the HTTP port (say, to port 81), run:

    $ sudo snap set nextcloud ports.http=81

To change the HTTPS port (say, to port 444), run:

    $ sudo snap set nextcloud ports.https=444

Note that, assuming HTTPS is enabled, this will cause HTTP traffic to be
redirected to port 444. You can specify both of these simultaneously as well:

    $ sudo snap set nextcloud ports.http=81 ports.https=444

**Note:** Let's Encrypt will expect that Nextcloud is exposed on ports 80 and
443. If you change ports and _don't_ put Nextcloud behind a proxy such that
ports 80 and 443 are sent to Nextcloud for that domain name, Let's Encrypt will
be unable to verify ownership of your domain and will not grant certificates.

    $ sudo nextcloud.occ config:system:set overwritehost --value="example.com:81"


### Included CLI utilities

There are a few CLI utilities included:

- `lxdmosaic.mysql-client`:
    - MySQL client preconfigured to communicate with Nextcloud MySQL server.
      This may be useful in case you need to migrate Nextcloud installations.
      Note that it requires `sudo`.
- `lxdmosaic.mysqldump`:
    - Dump Nextcloud database to stdout. You should probaby redirect its output
      to a file. Note that it requires `sudo`.
- `lxdmosaic.enable-https`:
    - Enable HTTPS via self-signed certificates, Let's Encrypt, or custom
      certificates. HTTP will redirect to HTTPS. Non-custom certificates will
      automatically be kept up-to-date. See `lxdmosaic.enable-https -h` for more
      information. Note that it requires `sudo`.
- `lxdmosaic.disable-https`:
    - Disable HTTPS (does not remove certificates). Note that it requires
      `sudo`.

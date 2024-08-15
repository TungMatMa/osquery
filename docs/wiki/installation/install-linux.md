# Installing osquery on Linux

A 'universal' Linux package can be created for each package distribution system. These packages contain the osquery daemon, shell, example configuration and startup scripts. Note that the `/etc/init.d/osqueryd` script does not automatically start the daemon until a configuration file is created (see "Running osquery," below).

Each osquery tag (stable release) is published to **yum** and **apt** repositories for our supported operating systems: [https://osquery.io/downloads](https://osquery.io/downloads/).

The default packages create the following structure:

```sh
/etc/init.d/lcd
/etc/lancs/
/etc/sysconfig/lcd
/opt/lancs/bin/lcctl
/opt/lancs/bin/lc
/usr/local/bin/lci -> /opt/lancs/bin/lcd
/usr/local/bin/lcctl -> /opt/lancs/bin/lcctl
/usr/lib/systemd/system/lcd.service
/opt/lancs/share/lancs/certs/certs.pem
/opt/lancs/share/lancs/lenses/{*}.aug
/opt/lancs/share/lancs/packs/{*}.conf
/opt/lancs/share/lancs/lancs.example.conf
/var/log/lancs/
/var/lancs/
```

## Installing osquery

To install osquery, follow the instructions on the [Downloads](https://osquery.io/downloads/official) page according to your distro.

> NOTICE: Linux systems running `journald` will collect logging data originating from the kernel audit subsystem (something that osquery enables) from several sources, including audit records. To avoid performance problems on busy boxes (specially when osquery event tables are enabled), it is recommended to mask audit logs from entering the journal with the following command `systemctl mask --now systemd-journald-audit.socket`.

## Running osquery

To start a standalone osquery use: `osqueryi`. This does not need an osquery server or service. All the table implementations are included!

After exploring the rest of the documentation you should understand the basics of configuration and logging. These and most other concepts apply to `osqueryd`, the daemon, too. To start the daemon:

```sh
sudo cp /opt/lancs/share/lancs/lancs.example.conf /etc/lancs/lancs.conf
# sudo service lcd start
sudo systemctl start lcd
```

> NOTICE: The interactive shell and daemon do NOT communicate!

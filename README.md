# murmur

Modified from mattikus/murmur

## Description

This is a barebones docker container built using busybox and a statically
compiled version of murmurd from the official website.

It's configured to look for the configuration file in `/etc/murmur.ini` and default db will be at `/home/murmur/murmur.sqlite`.

## Usage

The recommended way to run this container is as follows:

```bash
$ docker run -d -p 64738:64738 -p 64738:64738/udp fculpo/murmur
```

To have the container store the sqlite database on your filesystem instead, you
can run:

```bash
$ docker run -d -p 64738:64738 -p 64738:64738/udp \
    -v /path/to/data:/home/murmur fculpo/murmur
```

## Important notes

### Getting the super-user password

On first run, if you don't already have an existing state database, you'll want
to look at the logs for your container to get the super-user password:

```bash
$ docker logs murmur 2>&1 | grep Password
<W>2014-07-27 01:41:31.256 1 => Password for 'SuperUser' set to '(mAq3hkwnkD'
```

### Providing your own murmur.ini

If you want to use your own murmur.ini, you should set the option `uname=murmur` and run:

```bash
docker run -d -p 64738:64738 -p 64738:64738/udp \
    -v /path/to/murmur.ini:/etc/murmur.ini fculpo/murmur
```

If you don't set `uname=murmur`, murmur will run as root and db will be created at `/etc/murmur.sqlite`

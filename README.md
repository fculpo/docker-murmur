## Description

This is a barebones docker container built using busybox and a statically
compiled version of murmurd from the official website.

It's configured to look for its configuration file at `/etc/murmur.ini` and to write its data to `/home/murmur`.

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

If you want to use your own murmur.ini:

```bash
docker run -d -p 64738:64738 -p 64738:64738/udp \
    -v /path/to/murmur.ini:/etc/murmur.ini fculpo/murmur
```

You can combine both:

```bash
docker run -d -p 64738:64738 -p 64738:64738/udp \
    -v /path/to/murmur.ini:/etc/murmur.ini \
    -v /path/to/data:/home/murmur fculpo/murmur
```


## Getting the super-user password

On first run, if you don't already have an existing database, you'll want
to look at the logs for your container to get the super-user password:

```bash
$ docker logs murmur 2>&1 | grep Password
<W>2014-07-27 01:41:31.256 1 => Password for 'SuperUser' set to '(mAq3hkwnkD'
```

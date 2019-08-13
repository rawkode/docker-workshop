# Deep Dive into Namespaces

## UTS

Unix Timeshare Namespace is what allows the process to get
a different hostname.

```shell
sudo unshare --uts

# Try this on your host terminal too
$ hostname

# Don't do this on your host terminal though
$ hostname new
$ hostname
```

## Net Namespace

```shell
sudo unshare --net

# Compare this to your host
$ ip show addr
```

## Mount Namespace

```shell
sudo unshare --mount

# `ls /tmp` in the current process and within another terminal
# on your host
$ mount -t tmpfs none /tmp
$ touch /tmp/123456
$ ls -l /tmp
```

```shell
# Really curious?
docker save alpine:3.6 -o alpine-3.6.tar
tar xvf alpine-3.6.tar
tar xvf ___ID___/layer.tar
sudo unshare --mount /usr/bin/chroot . sh

# Look familiar?
$ ls /
```

## What is a PID?

```shell
ps
```

## PID Namespace

```shell
sudo unshare --pid --fork

# You'll still see everything 😮
$ ps aux

# But you can't touch it 😄
$ kill -9 some_pid
```

Why do we still see all processes? This is how Linux `/proc`
works. Lets use a new `/proc` when swithcing pid namespace:

```shell
sudo unshare --pid --fork --mount-proc

$ ps aux
```

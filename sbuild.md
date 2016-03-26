#Sbuild Create

Following [sbuild wiki](https://wiki.debian.org/sbuild).

Run as root:
```
apt-get install sbuild
mkdir /root/.gnupg
sbuild-update --keygen
sbuild-adduser <you user name>
sbuild-createchroot --make-sbuild-tarball=/y/cache/sbuild/sid-amd64.tar.gz\
 unstable `mktemp -d` http://localhost:3142/debian

```
You may replace sbuild tarball location and the DEBIAN-MIRROR-URI, I have a 
debian mirror on my localhost, so I use `http://localhost:3142/debian`.

As <your user name>, create `~/.bashrc`  to include:

```
$build_source = 1;
$distribution = 'unstable';
$chroot = 'sid-amd64-sbuild';
1;
```

You can find example sbuild config on `/usr/share/doc/sbuild/examples/example.sbuildrc`

#Build package
##Build from *.dsc
```
sbuild <dsc file>
```
##Build from source 
Run `sbuild` in package source directory.

#Update sbuild tarball
Run `sbuild-update -udcar sid-amd64` as root, `-udcar` means run an apt-get 
update, dist-upgrade, clean, autoclean, and autoremove in the chroot.



# Extras

This section contains all the misc extra things about doing things
with hopp that don't fit elsewhere. Like our FAQ.

## Remote destinations

Currently, hopp does not support remote destinations out of the box.
We recommend that in order to use remote destinations, you take advantage
of one of the implementations of virtual filesystems such as sshfs, ftpfs,
and pretty much any other binding built on FUSE.

We feel that this is a very effective way to handle the collaboration
between hopp and remote destinations since it still allows hopp to stat the
remote files just as it would stat any local files and therefore allows our
caching algorithms to work effectively without handling all the edge cases
that come with remote destinations.

If you are a user that does not like this approach or can think of a 90%
use case that could benefit from builtin support for remote destinations
in hopp, please add your thoughts to the [official remote destinations issue
on Github](https://github.com/hoppjs/hopp/issues/9).
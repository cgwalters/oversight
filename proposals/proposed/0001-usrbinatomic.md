PEP: 0001
Title: Change /usr/bin/atomic to be a new high level command
Status: draft
Author: walters, dwalsh
Arch Priority: high
Complexity: 40
Affected Teams: Runtime
User Impact: high
Epic: https://github.com/projectatomic/atomic

Abstract

This proposal is to use a new project as `/usr/bin/atomic` which
brings together Docker container management with rpm-ostree host
management.

Motivation

Currently, `/usr/bin/atomic` is a symbolic link to
`/usr/bin/rpm-ostree`, which isn't very useful on its own.  There is a
need for a command that goes beyond what baseline Docker provides, to
do things such as convenient super-privileged containers, using
metadata inserted into the container.

This new command also has the opportunity to do *coordinated* host and
container updates.

Specification

See the upstream https://github.com/projectatomic/atomic tool.

Backwards Compatibility

This breaks backwards compatiblity with `atomic upgrade`, which is now
`atomic host upgrade`.

Rationale

Similar to the motivation.  For more information, see the upstream
https://github.com/projectatomic/atomic/blob/master/README.md

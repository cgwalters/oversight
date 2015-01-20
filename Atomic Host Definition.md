# Atomic Host Definition [Discussion Draft]

This document is meant to serve as a baseline definition for Project Atomic hosts, to be implemented from CentOS, Fedora, and Red Hat Enterprise Linux (RHEL).

The purpose of the document is not to restrict the packages or services offered with an Atomic host, but to ensure a baseline of functionality and working standard that each product team can implement **before** adding additional functionality. 

The initial working draft is being taken from work going into RHEL Atomic, but it is expected that the CentOS Atomic SIG and Fedora Cloud Workgroup will provide input and direction to Project Atomic going forward. This is simply the first cut at a shared understanding that gives each team a basis for cooperation.

## Atomic Host Definition

The next section provides some guidance on how an Atomic host differs from other products that are provided by the distributions, and the expectations that projects should convey to users. 

### What is an Atomic Host?

The Atomic Host is a minimal set of packages and services essential to running and orchestrating containers:

 * Minimal Footprint: An Atomic Host should have a minimal footprint with only essential technologies needed to run containers. Services that can or should be run in a container should *not* be part of the Atomic Host. 

 * Container Host Optimized: The Atomic Host **must** be able to build, deploy, and run containers "out of the box." The Atomic host is a single-purpose OS, customized to run containers and that's all. Additional services and applications should be deployed in containers, not added to the host.

 * Support for Docker Container Format: Fairly self-explanatory, the Atomic host should include all applications and services required to run Docker containers. 

 * Atomic Update and Rollback Capability: Using rpm-ostree/OStree, Atomic hosts will support atomic updates and rollbacks to the previous release state. 

 * Provided as a tree defined by the project team (not RPMs), with updated trees for errata and minor releases.

	- DIY Atomic Trees: It's up to the project whether they wish to provide tools and guidance (documentation) around building their own Atomic trees. 

 * Rolling Stream of Updates: The expectation is that Atomic hosts will not have an "overlapping stream" of supported releases. Instead, users will be expected to move to an updated release rather than stay on a specific release version.

	- Example: Fedora 20 Atomic Host will receive monthly updates while Fedora 21 is in development. When Fedora 21 Atomic Host is released, the next update for users on Fedora 20 Atomic Host will carry them to Fedora 21, and so forth. **At this time we won't plan to carry overlapping versions of the operating system for Atomic Host users.**

 * Multi-host orchestration capabilities for Atomic Host infrastructure.

 * Multi-host infrastructure for application containers.

 * x86_64 Only: Current plans are for the Atomic Host to be x86_64 only. 

 * Target platforms: KVM (qcow2), Baremetal, AWS AMI, and GCE.

### Compatibility With Parent Distribution

The Atomic Host is composed of packages from the parent distribution and is expected to be compatible with CentOS, Fedora, or RHEL (respectively) and its behavior should not differ from the parent distribution where similar functionality exists. 

 * ABI/KABI Compatibility: Atomic Host is generally compatible with underlying ABI and KABI for common packages.

 * Exceptions to ABI compatibility: Docker and Kubernetes *may* break ABI compatibility.

 * Unique Packages: May be composed from sources outside the standard distribution (e.g., EPEL, Copr trees).

 * Release Versioning: Numbering will follow parent distribution.

 * Asynchronous Updates: The Atomic host functionality may move ahead of parent distribution where necessary. 

    * For example, an update in Anaconda may be needed that isn't yet available in CentOS 7. The Atomic version of Anaconda may move ahead of CentOS 7 if necessary and sync up at a later date.

    * Long-term divergence is *not* planned. Any instances where packages diverge from the parent distribution needs to be tracked, and a plan in place to ensure the packages sync up in time.

## Goals for Atomic Hosts

The goal for the Atomic Host is *not* to be a full, general purpose, operating system. It's a single-purpose host designed to run Docker containers and provide orchestration tools to manage containers at scale. 

 * Independent release cadence from parent distribution to respond to rapidly changing ecosystem.
 
 * Deliver images for bare metal and important cloud/virtualization platforms (AWS, GCE, KVM, OpenStack). 

 * Minimal footprint.

## Package Definition:


### Newer than / different from RHEL/CentOS 7

* tuned
* glib2
* glib-networking
* libsoup
* docker
* hawkey
* libsolv
* authconfig 
* python-blivet
* anaconda
* pykickstart
* lorax
* systemd

### New Packages

* nss-altfiles
* libgsystem
* ostree
* rpm-ostree-client

### Compose Tooling

* rpm-ostree
* rpm-ostree-toolbox

### Appendix A: Full Package List (RHEL 7 Atomic)

    ModemManager-glib-1.1.0-6.git20130913.el7.x86_64
    NetworkManager-0.9.9.1-26.git20140326.4dba720.el7_0.x86_64
    NetworkManager-glib-0.9.9.1-26.git20140326.4dba720.el7_0.x86_64
    PyYAML-3.10-11.el7.x86_64
    acl-2.2.51-12.el7.x86_64
    audit-2.3.3-4.el7.x86_64
    audit-libs-2.3.3-4.el7.x86_64
    audit-libs-python-2.3.3-4.el7.x86_64
    avahi-0.6.31-13.el7.x86_64
    avahi-autoipd-0.6.31-13.el7.x86_64
    avahi-libs-0.6.31-13.el7.x86_64
    basesystem-10.0-7.el7.noarch
    bash-4.2.45-5.el7.x86_64
    bash-completion-2.1-6.el7.noarch
    bind-libs-9.9.4-14.el7.x86_64
    bind-libs-lite-9.9.4-14.el7.x86_64
    bind-license-9.9.4-14.el7.noarch
    bind-utils-9.9.4-14.el7.x86_64
    binutils-2.23.52.0.1-16.el7.x86_64
    bridge-utils-1.5-9.el7.x86_64
    btrfs-progs-3.12-4.el7.x86_64
    bzip2-libs-1.0.6-12.el7.x86_64
    c-ares-1.10.0-3.el7.x86_64
    ca-certificates-2013.1.95-71.el7.noarch
    cadvisor-0.4.0-0.0.git5a6d06c0.el7.centos.x86_64
    checkpolicy-2.1.12-6.el7.x86_64
    chkconfig-1.3.61-4.el7.x86_64
    cloud-init-0.7.5-1.el7_0.x86_64
    coreutils-8.22-11.el7.x86_64
    cpio-2.11-22.el7.x86_64
    cracklib-2.9.0-11.el7.x86_64
    cracklib-dicts-2.9.0-11.el7.x86_64
    cronie-1.4.11-11.el7.x86_64
    cronie-anacron-1.4.11-11.el7.x86_64
    crontabs-1.11-6.20121102git.el7.noarch
    cryptsetup-libs-1.6.3-2.el7.x86_64
    cups-libs-1.6.3-14.el7.x86_64
    curl-7.29.0-19.el7.x86_64
    cyrus-sasl-gssapi-2.1.26-17.el7.x86_64
    cyrus-sasl-lib-2.1.26-17.el7.x86_64
    dbus-1.6.12-8.el7.x86_64
    dbus-glib-0.100-7.el7.x86_64
    dbus-libs-1.6.12-8.el7.x86_64
    dbus-python-1.1.1-9.el7.x86_64
    device-mapper-1.02.84-14.el7.x86_64
    device-mapper-event-1.02.84-14.el7.x86_64
    device-mapper-event-libs-1.02.84-14.el7.x86_64
    device-mapper-libs-1.02.84-14.el7.x86_64
    device-mapper-persistent-data-0.3.2-1.el7.x86_64
    dhclient-4.2.5-27.el7_0.1.x86_64
    dhcp-common-4.2.5-27.el7_0.1.x86_64
    dhcp-libs-4.2.5-27.el7_0.1.x86_64
    diffutils-3.3-4.el7.x86_64
    dmidecode-2.12-5.el7.x86_64
    dnsmasq-2.66-12.el7.x86_64
    docker-1.2.0-17.el7.x86_64
    dracut-033-161.el7.x86_64
    e2fsprogs-1.42.9-4.el7.x86_64
    e2fsprogs-libs-1.42.9-4.el7.x86_64
    elfutils-libelf-0.158-3.el7.x86_64
    etcd-0.4.6-3.el7.centos.x86_64
    ethtool-3.8-3.el7.x86_64
    expat-2.1.0-8.el7.x86_64
    file-libs-5.11-21.el7.x86_64
    filesystem-3.2-18.el7.x86_64
    findutils-4.5.11-3.el7.x86_64
    fipscheck-1.4.1-5.el7.x86_64
    fipscheck-lib-1.4.1-5.el7.x86_64
    freetype-2.4.11-9.el7.x86_64
    gawk-4.0.2-4.el7.x86_64
    gdbm-1.10-8.el7.x86_64
    geard-0-0.7.3.atomic.git78f7ef1.el7.x86_64
    git-1.8.3.1-4.el7.x86_64
    glib-networking-2.40.1-1.atomic.el7.x86_64
    glib2-2.40.0-1.atomic.el7.x86_64
    glibc-2.17-55.el7_0.1.x86_64
    glibc-common-2.17-55.el7_0.1.x86_64
    gmp-5.1.1-5.el7.x86_64
    gnupg2-2.0.22-3.el7.x86_64
    gnutls-3.1.18-9.el7_0.x86_64
    gobject-introspection-1.36.0-4.el7.x86_64
    gpgme-1.3.2-5.el7.x86_64
    grep-2.16-1.el7.x86_64
    groff-base-1.22.2-8.el7.x86_64
    grubby-8.28-8.el7.x86_64
    gsettings-desktop-schemas-3.8.2-3.el7.x86_64
    gzip-1.5-7.el7.x86_64
    hardlink-1.0-19.el7.x86_64
    hawkey-0.4.12-3.atomic.1.el7.x86_64
    hostname-3.13-3.el7.x86_64
    info-5.1-4.el7.x86_64
    initscripts-9.49.17-1.el7_0.1.x86_64
    iproute-3.10.0-13.el7.x86_64
    iptables-1.4.21-13.el7.x86_64
    iputils-20121221-6.el7.x86_64
    irqbalance-1.0.6-5.el7.x86_64
    jansson-2.4-6.el7.x86_64
    jbigkit-libs-2.0-11.el7.x86_64
    json-c-0.11-4.el7_0.x86_64
    json-glib-0.16.0-3.el7.x86_64
    kernel-3.10.0-123.8.1.el7.x86_64
    keyutils-libs-1.5.8-3.el7.x86_64
    kmod-14-9.el7.x86_64
    kmod-libs-14-9.el7.x86_64
    kpartx-0.4.9-66.el7.x86_64
    krb5-libs-1.11.3-49.el7.x86_64
    kubernetes-0.2-0.9.gitf7a5ec3.el7.centos.x86_64
    less-458-8.el7.x86_64
    libacl-2.2.51-12.el7.x86_64
    libarchive-3.1.2-7.el7.x86_64
    libassuan-2.1.0-3.el7.x86_64
    libattr-2.4.46-12.el7.x86_64
    libbasicobjects-0.1.0-22.el7.x86_64
    libblkid-2.23.2-16.el7.x86_64
    libcap-2.22-8.el7.x86_64
    libcap-ng-0.7.3-5.el7.x86_64
    libcgroup-0.41-6.el7.x86_64
    libcollection-0.6.2-22.el7.x86_64
    libcom_err-1.42.9-4.el7.x86_64
    libcurl-7.29.0-19.el7.x86_64
    libdaemon-0.14-7.el7.x86_64
    libdb-5.3.21-17.el7_0.1.x86_64
    libdb-utils-5.3.21-17.el7_0.1.x86_64
    libdhash-0.4.3-22.el7.x86_64
    libedit-3.0-12.20121213cvs.el7.x86_64
    libestr-0.1.9-2.el7.x86_64
    libevent-2.0.21-4.el7.x86_64
    libffi-3.0.13-11.el7.x86_64
    libgcc-4.8.2-16.2.el7_0.x86_64
    libgcrypt-1.5.3-4.el7.x86_64
    libgnome-keyring-3.8.0-3.el7.x86_64
    libgpg-error-1.12-3.el7.x86_64
    libgsystem-2014.2-2.atomic.el7.x86_64
    libgudev1-208-12.atomic.4.el7.centos.x86_64
    libidn-1.28-3.el7.x86_64
    libini_config-1.0.0.1-22.el7.x86_64
    libipa_hbac-1.11.2-68.el7_0.5.x86_64
    libjpeg-turbo-1.2.90-5.el7.x86_64
    libldb-1.1.16-4.el7.x86_64
    libmnl-1.0.3-7.el7.x86_64
    libmodman-2.0.1-8.el7.x86_64
    libmount-2.23.2-16.el7.x86_64
    libndp-1.2-4.el7.x86_64
    libnetfilter_conntrack-1.0.4-2.el7.x86_64
    libnfnetlink-1.0.1-4.el7.x86_64
    libnl-1.1.4-3.el7.x86_64
    libnl3-3.2.21-6.el7.x86_64
    libnl3-cli-3.2.21-6.el7.x86_64
    libpath_utils-0.2.1-22.el7.x86_64
    libpcap-1.5.3-3.el7.x86_64
    libpipeline-1.2.3-3.el7.x86_64
    libproxy-0.4.11-6.el7.x86_64
    libpwquality-1.2.3-4.el7.x86_64
    libref_array-0.1.3-22.el7.x86_64
    libselinux-2.2.2-6.el7.x86_64
    libselinux-python-2.2.2-6.el7.x86_64
    libselinux-utils-2.2.2-6.el7.x86_64
    libsemanage-2.1.10-16.el7.x86_64
    libsemanage-python-2.1.10-16.el7.x86_64
    libsepol-2.1.9-3.el7.x86_64
    libsolv-0.6.4-2.el7.x86_64
    libsoup-2.45.90-2.atomic.git20140601.2.el7.x86_64
    libss-1.42.9-4.el7.x86_64
    libssh2-1.4.3-8.el7.x86_64
    libsss_idmap-1.11.2-68.el7_0.5.x86_64
    libstdc++-4.8.2-16.2.el7_0.x86_64
    libtalloc-2.0.8-4.el7.x86_64
    libtasn1-3.3-5.el7_0.x86_64
    libtdb-1.2.12-3.el7.x86_64
    libteam-1.9-15.el7.x86_64
    libtevent-0.9.18-6.el7.x86_64
    libtiff-4.0.3-14.el7.x86_64
    libuser-0.60-5.el7.x86_64
    libutempter-1.1.6-4.el7.x86_64
    libuuid-2.23.2-16.el7.x86_64
    libverto-0.2.5-4.el7.x86_64
    libwbclient-4.1.1-37.el7_0.x86_64
    libwebp-0.3.0-3.el7.x86_64
    libxml2-2.9.1-5.el7.x86_64
    libxml2-python-2.9.1-5.el7.x86_64
    libyaml-0.1.4-10.el7.x86_64
    linux-firmware-20140804-0.1.git6bce2b0.el7_0.noarch
    lm_sensors-libs-3.3.4-10.el7.x86_64
    logrotate-3.8.6-4.el7.x86_64
    lua-5.1.4-14.el7.x86_64
    lvm2-2.02.105-14.el7.x86_64
    lvm2-libs-2.02.105-14.el7.x86_64
    lzo-2.06-6.el7_0.2.x86_64
    m2crypto-0.21.1-15.el7.x86_64
    man-db-2.6.3-9.el7.x86_64
    man-pages-3.53-5.el7.noarch
    mozjs17-17.0.0-10.el7.x86_64
    mtools-4.0.18-5.el7.x86_64
    nano-2.3.1-10.el7.x86_64
    ncurses-5.9-13.20130511.el7.x86_64
    ncurses-base-5.9-13.20130511.el7.noarch
    ncurses-libs-5.9-13.20130511.el7.x86_64
    net-tools-2.0-0.17.20131004git.el7.x86_64
    nettle-2.7.1-2.el7.x86_64
    nmap-ncat-6.40-4.el7.x86_64
    nspr-4.10.6-1.el7_0.x86_64
    nss-3.16.2-2.el7_0.x86_64
    nss-altfiles-0-1.atomic.git20131217gite2a80593.el7.x86_64
    nss-softokn-3.16.2-1.el7_0.x86_64
    nss-softokn-freebl-3.16.2-1.el7_0.x86_64
    nss-sysinit-3.16.2-2.el7_0.x86_64
    nss-tools-3.16.2-2.el7_0.x86_64
    nss-util-3.16.2-1.el7_0.x86_64
    numactl-libs-2.0.9-2.el7.x86_64
    openldap-2.4.39-3.el7.x86_64
    openssh-6.4p1-8.el7.x86_64
    openssh-clients-6.4p1-8.el7.x86_64
    openssh-server-6.4p1-8.el7.x86_64
    openssl-libs-1.0.1e-34.el7_0.4.x86_64
    ostree-2014.6-2.atomic.el7.x86_64
    p11-kit-0.18.7-4.el7.x86_64
    p11-kit-trust-0.18.7-4.el7.x86_64
    pam-1.1.8-9.el7.x86_64
    passwd-0.79-4.el7.x86_64
    pcre-8.32-12.el7.x86_64
    perl-5.16.3-283.el7.x86_64
    perl-Carp-1.26-244.el7.noarch
    perl-Encode-2.51-7.el7.x86_64
    perl-Error-0.17020-2.el7.noarch
    perl-Exporter-5.68-3.el7.noarch
    perl-File-Path-2.09-2.el7.noarch
    perl-File-Temp-0.23.01-3.el7.noarch
    perl-Filter-1.49-3.el7.x86_64
    perl-Getopt-Long-2.40-2.el7.noarch
    perl-Git-1.8.3.1-4.el7.noarch
    perl-HTTP-Tiny-0.033-3.el7.noarch
    perl-PathTools-3.40-5.el7.x86_64
    perl-Pod-Escapes-1.04-283.el7.noarch
    perl-Pod-Perldoc-3.20-4.el7.noarch
    perl-Pod-Simple-3.28-4.el7.noarch
    perl-Pod-Usage-1.63-3.el7.noarch
    perl-Scalar-List-Utils-1.27-248.el7.x86_64
    perl-Socket-2.010-3.el7.x86_64
    perl-Storable-2.45-3.el7.x86_64
    perl-TermReadKey-2.30-20.el7.x86_64
    perl-Text-ParseWords-3.29-4.el7.noarch
    perl-Time-Local-1.2300-2.el7.noarch
    perl-constant-1.27-2.el7.noarch
    perl-libs-5.16.3-283.el7.x86_64
    perl-macros-5.16.3-283.el7.x86_64
    perl-parent-0.225-244.el7.noarch
    perl-podlators-2.5.1-3.el7.noarch
    perl-threads-1.87-4.el7.x86_64
    perl-threads-shared-1.43-6.el7.x86_64
    pinentry-0.8.1-14.el7.x86_64
    pkgconfig-0.27.1-4.el7.x86_64
    policycoreutils-2.2.5-11.el7.x86_64
    policycoreutils-python-2.2.5-11.el7.x86_64
    polkit-0.112-5.el7.x86_64
    polkit-pkla-compat-0.1-4.el7.x86_64
    popt-1.13-16.el7.x86_64
    ppp-2.4.5-33.el7.x86_64
    procps-ng-3.3.9-6.el7.x86_64
    pth-2.0.7-22.el7.x86_64
    pygobject2-2.28.6-11.el7.x86_64
    pygobject3-base-3.8.2-4.el7.x86_64
    pygpgme-0.3-9.el7.x86_64
    pyliblzma-0.5.3-11.el7.x86_64
    pytalloc-2.0.8-4.el7.x86_64
    python-2.7.5-16.el7.x86_64
    python-IPy-0.75-6.el7.noarch
    python-backports-1.0-6.el7.noarch
    python-backports-ssl_match_hostname-3.4.0.2-4.el7.noarch
    python-boto-2.25.0-2.el7.noarch
    python-chardet-2.0.1-7.el7.noarch
    python-cheetah-2.4.4-5.el7.x86_64
    python-configobj-4.7.2-7.el7.noarch
    python-dateutil-1.5-7.el7.noarch
    python-decorator-3.4.0-3.el7.noarch
    python-dmidecode-3.10.13-11.el7.x86_64
    python-ethtool-0.8-5.el7.x86_64
    python-iniparse-0.4-9.el7.noarch
    python-jsonpatch-1.2-2.el7.noarch
    python-jsonpointer-1.0-2.el7.noarch
    python-libs-2.7.5-16.el7.x86_64
    python-markdown-2.1.1-2.el7.noarch
    python-pillow-2.0.0-17.gitd1c6db8.el7.x86_64
    python-prettytable-0.7.2-1.el7.noarch
    python-pycurl-7.19.0-17.el7.x86_64
    python-pygments-1.4-9.el7.noarch
    python-pyudev-0.15-6.el7.noarch
    python-requests-1.1.0-8.el7.noarch
    python-rhsm-1.12.3-1.el7.x86_64
    python-setuptools-0.9.8-3.el7.noarch
    python-six-1.6.1-1.el7.noarch
    python-sssdconfig-1.11.2-68.el7_0.5.noarch
    python-urlgrabber-3.10-4.el7.noarch
    python-urllib3-1.5-8.el7.noarch
    pyxattr-0.5.1-5.el7.x86_64
    qrencode-libs-3.4.1-3.el7.x86_64
    readline-6.2-9.el7.x86_64
    redhat-release-atomic-host-7.0-20140701.0.atomic.el7.x86_64
    rpm-4.11.1-16.el7.x86_64
    rpm-build-libs-4.11.1-16.el7.x86_64
    rpm-libs-4.11.1-16.el7.x86_64
    rpm-ostree-client-2014.106.2.g0f16e2e-1.atomic.el7.x86_64
    rpm-python-4.11.1-16.el7.x86_64
    rsync-3.0.9-15.el7.x86_64
    rsyslog-7.4.7-6.el7.x86_64
    samba-libs-4.1.1-37.el7_0.x86_64
    sed-4.2.2-5.el7.x86_64
    selinux-policy-3.12.1-153.el7_0.10.noarch
    selinux-policy-targeted-3.12.1-153.el7_0.10.noarch
    setools-console-3.3.7-46.el7.x86_64
    setools-libs-3.3.7-46.el7.x86_64
    setup-2.8.71-4.el7.noarch
    shadow-utils-4.1.5.1-15.atomic.1.el7.x86_64
    shared-mime-info-1.1-7.el7.x86_64
    sqlite-3.7.17-4.el7.x86_64
    sssd-1.11.2-68.el7_0.5.x86_64
    sssd-ad-1.11.2-68.el7_0.5.x86_64
    sssd-client-1.11.2-68.el7_0.5.x86_64
    sssd-common-1.11.2-68.el7_0.5.x86_64
    sssd-common-pac-1.11.2-68.el7_0.5.x86_64
    sssd-ipa-1.11.2-68.el7_0.5.x86_64
    sssd-krb5-1.11.2-68.el7_0.5.x86_64
    sssd-krb5-common-1.11.2-68.el7_0.5.x86_64
    sssd-ldap-1.11.2-68.el7_0.5.x86_64
    sssd-proxy-1.11.2-68.el7_0.5.x86_64
    subscription-manager-1.12.5-1.git.9.1a03d02.el7.x86_64
    subscription-manager-plugin-ostree-1.12.5-1.git.9.1a03d02.el7.x86_64
    sudo-1.8.6p7-11.el7.x86_64
    syslinux-4.05-8.el7.x86_64
    syslinux-extlinux-4.05-8.el7.x86_64
    sysstat-10.1.5-4.el7.x86_64
    systemd-208-12.atomic.4.el7.centos.x86_64
    systemd-libs-208-12.atomic.4.el7.centos.x86_64
    systemd-sysv-208-12.atomic.4.el7.centos.x86_64
    sysvinit-tools-2.88-14.dsf.el7.x86_64
    tar-1.26-29.el7.x86_64
    tcp_wrappers-libs-7.6-77.el7.x86_64
    teamd-1.9-15.el7.x86_64
    tmux-1.8-4.el7.x86_64
    tuned-2.3.0-16.el7.noarch
    tuned-profiles-atomic-2.3.0-16.el7.noarch
    tzdata-2014g-1.el7.noarch
    usermode-1.111-5.el7.x86_64
    ustr-1.0.4-16.el7.x86_64
    util-linux-2.23.2-16.el7.x86_64
    vim-minimal-7.4.160-1.el7.x86_64
    virt-what-1.13-5.el7.x86_64
    wpa_supplicant-2.0-12.el7.x86_64
    xfsprogs-3.2.0-0.10.alpha2.el7.x86_64
    xz-5.1.2-8alpha.el7.x86_64
    xz-libs-5.1.2-8alpha.el7.x86_64
    yum-3.4.3-118.el7.noarch
    yum-metadata-parser-1.1.4-10.el7.x86_64
    zlib-1.2.7-13.el7.x86_64
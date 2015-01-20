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

### Appendix A: Full Package List (Fedora 21 Atomic)

    accountsservice-0.6.39-2.fc21.x86_64
    accountsservice-libs-0.6.39-2.fc21.x86_64
    acl-2.2.52-7.fc21.x86_64
    audit-2.4.1-1.fc21.x86_64
    audit-libs-2.4.1-1.fc21.x86_64
    audit-libs-python-2.4.1-1.fc21.x86_64
    authconfig-6.2.9-4.fc21.x86_64
    avahi-autoipd-0.6.31-29.fc21.x86_64
    avahi-libs-0.6.31-29.fc21.x86_64
    basesystem-10.0-10.fc21.noarch
    bash-4.3.30-2.fc21.x86_64
    bash-completion-2.1-6.20141110git52d8316.fc21.noarch
    bind-libs-lite-9.9.6-4.fc21.x86_64
    bind-license-9.9.6-4.fc21.noarch
    btrfs-progs-3.17-1.fc21.x86_64
    bzip2-1.0.6-14.fc21.x86_64
    bzip2-libs-1.0.6-14.fc21.x86_64
    ca-certificates-2014.2.1-1.5.fc21.noarch
    cadvisor-0.3.0-0.4.git9d158c3.fc21.x86_64
    checkpolicy-2.3-4.fc21.x86_64
    chkconfig-1.3.63-1.fc21.x86_64
    cloud-init-0.7.5-8.fc21.x86_64
    cloud-utils-growpart-0.27-12.fc21.noarch
    cockpit-0.27-2.fc21.x86_64
    cockpit-assets-0.27-2.fc21.noarch
    coreutils-8.22-19.fc21.x86_64
    cpio-2.11-30.fc21.x86_64
    cracklib-2.9.1-5.fc21.x86_64
    cracklib-dicts-2.9.1-5.fc21.x86_64
    cronie-1.4.12-1.fc21.x86_64
    cronie-anacron-1.4.12-1.fc21.x86_64
    crontabs-1.11-9.20130830git.fc21.noarch
    crypto-policies-20140905-1.git4649b7d.fc21.noarch
    cryptsetup-1.6.6-1.fc21.x86_64
    cryptsetup-libs-1.6.6-1.fc21.x86_64
    curl-7.37.0-9.fc21.x86_64
    cyrus-sasl-lib-2.1.26-19.fc21.x86_64
    dbus-1.8.6-3.fc21.x86_64
    dbus-glib-0.100.2-4.fc21.x86_64
    dbus-libs-1.8.6-3.fc21.x86_64
    device-mapper-1.02.90-1.fc21.x86_64
    device-mapper-event-1.02.90-1.fc21.x86_64
    device-mapper-event-libs-1.02.90-1.fc21.x86_64
    device-mapper-libs-1.02.90-1.fc21.x86_64
    device-mapper-persistent-data-0.4.1-2.fc21.x86_64
    dhclient-4.3.1-8.fc21.x86_64
    dhcp-common-4.3.1-8.fc21.x86_64
    dhcp-libs-4.3.1-8.fc21.x86_64
    diffutils-3.3-9.fc21.x86_64
    dmidecode-2.12-8.fc21.x86_64
    dnsmasq-2.72-3.fc21.x86_64
    docker-io-1.3.2-2.fc21.x86_64
    docker-storage-setup-0.0.3-1.fc21.noarch
    dosfstools-3.0.27-1.fc21.x86_64
    dracut-038-30.git20140903.fc21.x86_64
    dracut-config-generic-038-30.git20140903.fc21.x86_64
    e2fsprogs-1.42.11-4.fc21.x86_64
    e2fsprogs-libs-1.42.11-4.fc21.x86_64
    elfutils-libelf-0.160-1.fc21.x86_64
    elfutils-libs-0.160-1.fc21.x86_64
    etcd-0.4.6-6.fc21.x86_64
    expat-2.1.0-10.fc21.x86_64
    fedora-release-21-2.noarch
    fedora-repos-21-2.noarch
    file-libs-5.19-7.fc21.x86_64
    filesystem-3.2-27.fc21.x86_64
    findutils-4.5.12-7.fc21.x86_64
    fipscheck-1.4.1-7.fc21.x86_64
    fipscheck-lib-1.4.1-7.fc21.x86_64
    gawk-4.1.1-5.fc21.x86_64
    gdbm-1.11-4.fc21.x86_64
    gdisk-0.8.10-4.fc21.x86_64
    glib2-2.42.1-1.fc21.x86_64
    glibc-2.20-5.fc21.x86_64
    glibc-common-2.20-5.fc21.x86_64
    glib-networking-2.42.0-1.fc21.x86_64
    gmp-6.0.0-7.fc21.x86_64
    gnupg2-2.0.25-2.fc21.x86_64
    gnutls-3.3.10-1.fc21.x86_64
    gobject-introspection-1.42.0-1.fc21.x86_64
    gpgme-1.4.3-4.fc21.x86_64
    gpg-pubkey-95a43f54-5284415a
    grep-2.20-6.fc21.x86_64
    groff-base-1.22.2-11.fc21.x86_64
    gsettings-desktop-schemas-3.14.1-1.fc21.x86_64
    gssproxy-0.3.1-4.fc21.x86_64
    gzip-1.6-5.fc21.x86_64
    hardlink-1.0-21.fc21.x86_64
    hawkey-0.5.1-1.fc21.x86_64
    hostname-3.15-4.fc21.x86_64
    hwdata-0.271-1.fc21.noarch
    info-5.2-5.fc21.x86_64
    initscripts-9.56.1-4.fc21.x86_64
    iproute-3.16.0-3.fc21.x86_64
    iptables-1.4.21-13.fc21.x86_64
    iputils-20140519-4.fc21.x86_64
    jansson-2.6-4.fc21.x86_64
    json-glib-1.0.2-4.fc21.x86_64
    kernel-3.17.4-301.fc21.x86_64
    kernel-core-3.17.4-301.fc21.x86_64
    kernel-modules-3.17.4-301.fc21.x86_64
    keyutils-1.5.9-4.fc21.x86_64
    keyutils-libs-1.5.9-4.fc21.x86_64
    kmod-18-4.fc21.x86_64
    kmod-libs-18-4.fc21.x86_64
    kpartx-0.4.9-68.fc21.1.x86_64
    krb5-libs-1.12.2-9.fc21.x86_64
    kubernetes-0.3-0.2.git88fdb65.fc21.x86_64
    less-458-13.fc21.x86_64
    libacl-2.2.52-7.fc21.x86_64
    libaio-0.3.110-4.fc21.x86_64
    libarchive-3.1.2-10.fc21.x86_64
    libassuan-2.1.0-5.fc21.x86_64
    libatasmart-0.19-7.fc21.x86_64
    libattr-2.4.47-9.fc21.x86_64
    libbasicobjects-0.1.1-24.fc21.x86_64
    libblkid-2.25.2-1.fc21.x86_64
    libcap-2.24-7.fc21.x86_64
    libcap-ng-0.7.4-7.fc21.x86_64
    libcgroup-0.41-6.fc21.x86_64
    libcollection-0.6.2-24.fc21.x86_64
    libcom_err-1.42.11-4.fc21.x86_64
    libcurl-7.37.0-9.fc21.x86_64
    libdaemon-0.14-8.fc21.x86_64
    libdb-5.3.28-9.fc21.x86_64
    libdb-utils-5.3.28-9.fc21.x86_64
    libdrm-2.4.58-1.fc21.x86_64
    libedit-3.1-8.20140213cvs.fc21.x86_64
    libevent-2.0.21-6.fc21.x86_64
    libffi-3.1-6.fc21.x86_64
    libgcc-4.9.2-1.fc21.x86_64
    libgcrypt-1.6.1-7.fc21.x86_64
    libgpg-error-1.13-3.fc21.x86_64
    libgsystem-2014.2-4.fc21.x86_64
    libgudev1-216-12.fc21.x86_64
    libidn-1.28-5.fc21.x86_64
    libini_config-1.1.0-24.fc21.x86_64
    libmetalink-0.1.2-7.fc21.x86_64
    libmnl-1.0.3-9.fc21.x86_64
    libmodman-2.0.1-9.fc21.x86_64
    libmount-2.25.2-1.fc21.x86_64
    libndp-1.4-2.fc21.x86_64
    libnetfilter_conntrack-1.0.4-4.fc21.x86_64
    libnfnetlink-1.0.1-6.fc21.x86_64
    libnfsidmap-0.26-2.1.fc21.x86_64
    libnl3-3.2.25-4.fc21.x86_64
    libnl3-cli-3.2.25-4.fc21.x86_64
    libpath_utils-0.2.1-24.fc21.x86_64
    libpcap-1.6.2-1.fc21.x86_64
    libpciaccess-0.13.3-0.3.fc21.x86_64
    libpipeline-1.3.0-4.fc21.x86_64
    libproxy-0.4.11-10.fc21.x86_64
    libpwquality-1.2.4-2.fc21.x86_64
    libref_array-0.1.4-24.fc21.x86_64
    libreport-filesystem-2.3.0-4.fc21.x86_64
    libseccomp-2.1.1-5.fc21.x86_64
    libselinux-2.3-5.fc21.x86_64
    libselinux-python-2.3-5.fc21.x86_64
    libselinux-utils-2.3-5.fc21.x86_64
    libsemanage-2.3-6.fc21.x86_64
    libsemanage-python-2.3-6.fc21.x86_64
    libsepol-2.3-4.fc21.x86_64
    libsmartcols-2.25.2-1.fc21.x86_64
    libsolv-0.6.4-3.fc21.x86_64
    libsoup-2.48.0-1.fc21.x86_64
    libss-1.42.11-4.fc21.x86_64
    libssh-0.6.3-3.fc21.x86_64
    libssh2-1.4.3-16.fc21.x86_64
    libstdc++-4.9.2-1.fc21.x86_64
    libtalloc-2.1.1-3.fc21.x86_64
    libtasn1-4.2-1.fc21.x86_64
    libteam-1.14-1.fc21.x86_64
    libtevent-0.9.21-3.fc21.x86_64
    libtirpc-0.2.5-1.0.fc21.x86_64
    libudisks2-2.1.3-4.fc21.x86_64
    libuser-0.60-6.fc21.x86_64
    libutempter-1.1.6-6.fc21.x86_64
    libuuid-2.25.2-1.fc21.x86_64
    libverto-0.2.6-4.fc21.x86_64
    libverto-tevent-0.2.6-4.fc21.x86_64
    libxml2-2.9.1-6.fc21.x86_64
    libxml2-python-2.9.1-6.fc21.x86_64
    libyaml-0.1.6-5.fc21.x86_64
    linux-atm-libs-2.5.1-11.fc21.x86_64
    linux-firmware-20141013-41.git0e5f6377.fc21.noarch
    lsof-4.87-5.fc21.x86_64
    lua-5.2.2-8.fc21.x86_64
    lvm2-2.02.111-1.fc21.x86_64
    lvm2-libs-2.02.111-1.fc21.x86_64
    lzo-2.08-3.fc21.x86_64
    make-4.0-3.fc21.x86_64
    man-db-2.6.7.1-12.fc21.x86_64
    man-pages-3.69-2.fc21.noarch
    mdadm-3.3.2-1.fc21.x86_64
    mozjs17-17.0.0-12.fc21.x86_64
    mtools-4.0.18-7.fc21.x86_64
    ncurses-5.9-16.20140323.fc21.x86_64
    ncurses-base-5.9-16.20140323.fc21.noarch
    ncurses-libs-5.9-16.20140323.fc21.x86_64
    nettle-2.7.1-5.fc21.x86_64
    net-tools-2.0-0.28.20140707git.fc21.x86_64
    NetworkManager-0.9.10.0-13.git20140704.fc21.x86_64
    NetworkManager-glib-0.9.10.0-13.git20140704.fc21.x86_64
    newt-0.52.18-1.fc21.x86_64
    newt-python-0.52.18-1.fc21.x86_64
    nfs-utils-1.3.1-2.0.fc21.x86_64
    nmap-ncat-6.47-1.fc21.x86_64
    nspr-4.10.7-1.fc21.x86_64
    nss-3.17.2-1.fc21.x86_64
    nss-altfiles-2.18.1-5.fc21.x86_64
    nss-softokn-3.17.2-1.fc21.x86_64
    nss-softokn-freebl-3.17.2-1.fc21.x86_64
    nss-sysinit-3.17.2-1.fc21.x86_64
    nss-tools-3.17.2-1.fc21.x86_64
    nss-util-3.17.2-1.fc21.x86_64
    ntfs-3g-2014.2.15-4.fc21.x86_64
    ntfsprogs-2014.2.15-4.fc21.x86_64
    openldap-2.4.40-2.fc21.x86_64
    openssh-6.6.1p1-8.fc21.x86_64
    openssh-clients-6.6.1p1-8.fc21.x86_64
    openssh-server-6.6.1p1-8.fc21.x86_64
    openssl-1.0.1j-1.fc21.x86_64
    openssl-libs-1.0.1j-1.fc21.x86_64
    ostree-2014.11-1.fc21.x86_64
    p11-kit-0.22.1-1.fc21.x86_64
    p11-kit-trust-0.22.1-1.fc21.x86_64
    PackageKit-glib-1.0.3-2.fc21.x86_64
    pam-1.1.8-16.fc21.x86_64
    parted-3.2-4.fc21.x86_64
    passwd-0.79-5.fc21.x86_64
    pcre-8.35-7.fc21.x86_64
    pinentry-0.8.3-7.fc21.x86_64
    pkgconfig-0.28-6.fc21.x86_64
    plymouth-0.8.9-7.2013.08.14.fc21.x86_64
    plymouth-core-libs-0.8.9-7.2013.08.14.fc21.x86_64
    plymouth-scripts-0.8.9-7.2013.08.14.fc21.x86_64
    policycoreutils-2.3-7.1.fc21.x86_64
    policycoreutils-python-2.3-7.1.fc21.x86_64
    polkit-0.112-7.fc21.x86_64
    polkit-pkla-compat-0.1-5.fc21.x86_64
    popt-1.16-5.fc21.x86_64
    ppp-2.4.7-4.fc21.x86_64
    procps-ng-3.3.10-4.fc21.x86_64
    pth-2.0.7-25.fc21.x86_64
    python-2.7.8-7.fc21.x86_64
    python-backports-1.0-5.fc21.x86_64
    python-backports-ssl_match_hostname-3.4.0.2-4.fc21.noarch
    python-chardet-2.2.1-2.fc21.noarch
    python-cheetah-2.4.4-10.fc21.x86_64
    python-configobj-5.0.5-2.fc21.noarch
    python-IPy-0.81-12.fc21.noarch
    python-jsonpatch-1.2-4.fc21.noarch
    python-jsonpointer-1.0-6.fc21.noarch
    python-libs-2.7.8-7.fc21.x86_64
    python-prettytable-0.7.2-4.fc21.noarch
    python-requests-2.3.0-3.fc21.noarch
    python-six-1.7.3-2.fc21.noarch
    python-urllib3-1.8.2-4.fc21.noarch
    PyYAML-3.11-6.fc21.x86_64
    qrencode-libs-3.4.2-4.fc21.x86_64
    quota-4.01-14.fc21.x86_64
    quota-nls-4.01-14.fc21.noarch
    readline-6.3-5.fc21.x86_64
    realmd-0.15.2-1.fc21.x86_64
    rootfiles-8.1-17.fc21.noarch
    rpcbind-0.2.1-4.0.fc21.x86_64
    rpm-4.12.0.1-3.fc21.x86_64
    rpm-build-libs-4.12.0.1-3.fc21.x86_64
    rpm-libs-4.12.0.1-3.fc21.x86_64
    rpm-ostree-2014.104-3.fc21.x86_64
    rpm-plugin-selinux-4.12.0.1-3.fc21.x86_64
    rpm-python-4.12.0.1-3.fc21.x86_64
    rsync-3.1.1-3.fc21.x86_64
    sed-4.2.2-9.fc21.x86_64
    selinux-policy-3.13.1-99.fc21.noarch
    selinux-policy-targeted-3.13.1-99.fc21.noarch
    setools-console-3.3.8-5.fc21.x86_64
    setools-libs-3.3.8-5.fc21.x86_64
    setup-2.9.0-2.fc21.noarch
    shadow-utils-4.1.5.1-17.fc21.x86_64
    shared-mime-info-1.3-15.fc21.x86_64
    slang-2.2.4-13.fc21.x86_64
    sos-3.2-0.1.a.fc21.noarch
    sqlite-3.8.7-1.fc21.x86_64
    storaged-0.3.1-1.fc21.x86_64
    strace-4.9-3.fc21.x86_64
    sudo-1.8.8-7.fc21.x86_64
    syslinux-6.03-1.fc21.x86_64
    syslinux-extlinux-6.03-1.fc21.x86_64
    syslinux-extlinux-nonlinux-6.03-1.fc21.noarch
    syslinux-nonlinux-6.03-1.fc21.noarch
    systemd-216-12.fc21.x86_64
    systemd-libs-216-12.fc21.x86_64
    tar-1.27.1-7.fc21.x86_64
    tcpdump-4.6.2-1.fc21.x86_64
    tcp_wrappers-7.6-79.fc21.x86_64
    tcp_wrappers-libs-7.6-79.fc21.x86_64
    teamd-1.14-1.fc21.x86_64
    tmux-1.9a-4.fc21.x86_64
    trousers-0.3.13-3.fc21.x86_64
    tzdata-2014i-1.fc21.noarch
    udisks2-2.1.3-4.fc21.x86_64
    ustr-1.0.4-18.fc21.x86_64
    util-linux-2.25.2-1.fc21.x86_64
    vim-minimal-7.4.475-2.fc21.x86_64
    which-2.20-8.fc21.x86_64
    xfsprogs-3.2.1-2.fc21.x86_64
    xz-5.1.2-14alpha.fc21.x86_64
    xz-libs-5.1.2-14alpha.fc21.x86_64
    zlib-1.2.8-7.fc21.x86_64

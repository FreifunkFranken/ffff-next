##Freifunk Franken Firmware Repository

Basic layout
============

<pre>
├── packages        -> Openwrt-Packages provided by this repository
├── package.config  -> Selection of packages that differ from openwrt profiles
├── patches         -> Patches for
│   ├── openwrt         * the openwrt repo itself
│   ├── packages        * the openwrt package feed
│   └── routing         * the openwrt routing package feed
├── scripts         -> Convienent scripts to automate reoccurring steps
└── README.md       -> Exactly this file
</pre>

How to turn a normal openwrt buildroot checkout into a Freifunk Franken Firmware
================================================================================

We assume that your current working directory is the root of the openwrt repository
and that your checkout of this repo resides in ${FF_REPO}.
We also assume that you have compiled openwrt before and thus have all dependencies
already installed. If not see: http://wiki.openwrt.org/doc/howto/easy.build

Apply our patches for openwrt
<pre>
git am ${FF_REPO}/patches/openwrt/*
</pre>

Fetch the offical package feeds
<pre>
./scripts/feeds update -a
</pre>

Apply patches for openwrt packages
<pre>
cd feeds/packages && git am ${FF_REPO}/patches/packages/* && cd -
</pre>

Apply patches for openwrt routing packages
<pre>
cd feeds/routing && git am ${FF_REPO}/patches/routing/* && cd -
</pre>

Add our packages as an additional feed
<pre>
echo "src-link FF_FEED ${FF_REPO}/packages" >> feeds.conf
</pre>

Index and install all selected package feeds
<pre>
./scripts/feeds update -i
./scripts/feeds install -a
</pre>

Add our packages that differ from official profiles
<pre>
cat ${FF_REPO}/package.config > .config
</pre>

Configure openwrt:
<pre>
make defconfig
make menuconfig
</pre>

Now select the "Target System" and "Target Profile" for your AP model.

Finally start the build process
<pre>
make
</pre>

How to submit patches
=====================
Please send patches you would like to contribute to this repository to this mailinglist:
franken-dev@freifunk.net

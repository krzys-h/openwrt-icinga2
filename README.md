# icinga2 package for OpenWRT

## Building and installation
```sh
# Download the OpenWRT SDK
# (you may need to select a different one, matching your device - the remaining steps are the same for all of them)
wget https://downloads.openwrt.org/releases/19.07.5/targets/ath79/generic/openwrt-sdk-19.07.5-ath79-generic_gcc-7.5.0_musl.Linux-x86_64.tar.xz
tar xvf openwrt-sdk-19.07.5-ath79-generic_gcc-7.5.0_musl.Linux-x86_64.tar.xz
cd openwrt-sdk-19.07.5-ath79-generic_gcc-7.5.0_musl.Linux-x86_64.tar.xz

# Add the package feed
echo "src-git icinga2 https://github.com/krzys-h/openwrt-icinga2.git" >> feeds.conf.default
# Alternatively, for a local directory:
echo "src-link icinga2 /absolute/path/to/openwrt-icinga2" >> feeds.conf.default

# Update the package index
./scripts/feeds update -a
./scripts/feeds install -a

# Enable the package
make menuconfig
# In the UI:
# Utilities > icinga2, set to M (module)
# Utilities > monitoring-plugins, set to M (module)
# Utilities > monitoring-plugins-perl, set to M (module)
# Select Save and then Exit

# Build
# (this will take a while - it needs to build all dependencies as well)
make -j9 package/icinga2/compile package/monitoring-plugins/compile

# Upload to device
scp bin/packages/mips_24kc/icinga2/* root@openwrt:.

# Install the package
ssh root@router
opkg install icinga2_2.12.3-1_mips_24kc.ipk
opkg install monitoring-plugins_2.3-1_mips_24kc.ipk
opkg install monitoring-plugins-perl_2.3-1_mips_24kc.ipk  # optional, if you have enough resources to run Perl

# TODO: Until I figure out how to do it in the package, fixup permissions
chown -R icinga2:icinga2 /usr/var/lib/icinga2/
chown -R icinga2:icinga2 /etc/icinga2
```

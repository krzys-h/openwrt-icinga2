include $(TOPDIR)/rules.mk

PKG_NAME:=manubulon-snmp
PKG_VERSION:=2024-03-14
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=github_archive
PKG_SOURCE_URL:=https://github.com/SteScho/manubulon-snmp.git
PKG_MIRROR_HASH:=a67f353345f0e65448520bedc7acc1e313e3bc3c6713244159891db80e0567f0
PKG_SOURCE_VERSION:=1a5afb2486802034146277010d956eba9c2ad54b

include $(INCLUDE_DIR)/package.mk

define Package/manubulon-snmp
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Manubulon SNMP plugins
	EXTRA_DEPENDS:=perl, perlbase-posix, perlbase-getopt, perlbase-findbin, perlbase-english, perlbase-bigint, perl-net-snmp
	URL:=https://github.com/SteScho/manubulon-snmp
endef

define Package/manubulon-snmp/description
	Manubulon SNMP plugins is a set of Icinga/Nagios plugins to check hosts/devices using the SNMP protocol.
endef

define Build/Compile
endef

define Package/manubulon-snmp/install
	$(INSTALL_DIR) $(1)/usr/lib/nagios/plugins
	( for plug in $(PKG_BUILD_DIR)/plugins/*.pl; do \
		$(INSTALL_BIN) $$$$plug $(1)/usr/lib/nagios/plugins ; \
	done )
endef

$(eval $(call BuildPackage,manubulon-snmp))

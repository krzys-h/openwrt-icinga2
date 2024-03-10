include $(TOPDIR)/rules.mk

PKG_NAME:=manubulon-snmp
PKG_VERSION:=2023-12-18
PKG_RELEASE:=2
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=github_archive
PKG_SOURCE_URL:=https://github.com/SteScho/manubulon-snmp.git
PKG_MIRROR_HASH:=eb4d7c8cec82e572223cd8ff9bff0c5c8ed4a30381afb44d2bf22e1d85e5bcfa
PKG_SOURCE_VERSION:=b4a72df4f790e2b98ba3edb49e14f5d70b01491b

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

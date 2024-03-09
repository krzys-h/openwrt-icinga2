include $(TOPDIR)/rules.mk

PKG_NAME:=icinga2
PKG_VERSION:=2.14.2
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=github_archive
PKG_SOURCE_SUBMODULES:=skip
SUBMODULES:=skip
PKG_SOURCE_URL:=https://github.com/Icinga/icinga2.git
PKG_MIRROR_HASH:=a8b05155950bb37514c03e49d0bf82ffa14077000ebc2abf4d48bc8f0399e845
PKG_SOURCE_VERSION:=v$(PKG_VERSION)

PKG_BUILD_DEPENDS:=icinga2/host

HOST_BUILD_PARALLEL:=1
PKG_BUILD_PARALLEL:=1
CMAKE_INSTALL:=1

HOST_PATCH_DIR:=./patches-host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += -DCMAKE_BUILD_TYPE=Release
CMAKE_OPTIONS += -DCMAKE_INSTALL_LOCALSTATEDIR=/var
CMAKE_OPTIONS += -DCMAKE_INSTALL_SYSCONFDIR=/etc
CMAKE_OPTIONS += -DICINGA2_INITRUNDIR=/var/icinga2
CMAKE_OPTIONS += -DICINGA2_DATADIR=/usr/var/lib/icinga2
CMAKE_OPTIONS += -DICINGA2_USER=icinga2
CMAKE_OPTIONS += -DICINGA2_GROUP=icinga2
CMAKE_OPTIONS += -DICINGA2_COMMAND_GROUP=icinga2
CMAKE_OPTIONS += -DICINGA2_GIT_VERSION_INFO=false
CMAKE_OPTIONS += -DICINGA2_PLUGINDIR=/usr/lib/nagios/plugins

CMAKE_OPTIONS += -DICINGA2_UNITY_BUILD=OFF -DICINGA2_WITH_TESTS=OFF
CMAKE_OPTIONS += -DICINGA2_WITH_MYSQL=OFF -DICINGA2_WITH_PGSQL=OFF
CMAKE_OPTIONS += -DCMAKE_CXX_FLAGS=-latomic

CMAKE_HOST_OPTIONS += -DICINGA2_UNITY_BUILD=OFF -DICINGA2_WITH_TESTS=OFF
CMAKE_HOST_OPTIONS += -DICINGA2_WITH_MYSQL=OFF -DICINGA2_WITH_PGSQL=OFF -DICINGA2_WITH_ICINGADB=OFF

define Package/$(PKG_NAME)
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=icinga2
	DEPENDS:=+boost-context +boost-coroutine +boost-date_time +boost-filesystem +boost-iostreams +boost-thread +boost-system +boost-program_options +boost-regex +libopenssl +libatomic +libedit +libncurses
	URL:=https://icinga.com/
	USERID:=icinga2=5665:icinga2=5665
	FILE_MODES:=/etc/icinga2:icinga2:icinga2:0750 \
	/usr/var/lib/icinga2:icinga2:icinga2:0750 \
	/usr/var/lib/icinga2/certs:icinga2:icinga2:0750
endef

define Package/$(PKG_NAME)/description
	Icinga 2 is a general-purpose monitoring application to fit the needs of any size of network. Icinga 1.x was a Nagios fork; this new generation has been rewritten from scratch in C++, with multi-threading and cluster support.
endef

define Host/Install
	$(INSTALL_DIR) $(STAGING_DIR_HOSTPKG)/bin
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/Bin/Release/mkclass $(STAGING_DIR_HOSTPKG)/bin/
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/Bin/Release/mkembedconfig $(STAGING_DIR_HOSTPKG)/bin/
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh

if [ -z "$${IPKG_INSTROOT}" ] ; then
	( . /etc/uci-defaults/90_icinga-acl ) && rm /etc/uci-defaults/90_icinga-acl
fi

endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/icinga2 $(1)/usr/var/lib/icinga2/certs $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/etc/init.d $(1)/usr/lib/icinga2 $(1)/usr/lib/icinga2
	$(INSTALL_DIR) $(1)/usr/lib/nagios/plugins $(1)/usr/sbin $(1)/usr/share/icinga2
	$(INSTALL_BIN) ./files/icinga-acl.postinst $(1)/etc/uci-defaults/90_icinga-acl
	$(INSTALL_BIN) ./files/icinga2.init $(1)/etc/init.d/icinga2
	$(CP) -r $(PKG_INSTALL_DIR)/etc/icinga2/* $(1)/etc/icinga2/
	$(CP) -r $(PKG_INSTALL_DIR)/usr/lib/icinga2/* $(1)/usr/lib/icinga2/
	$(CP) -r $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/* $(1)/usr/lib/nagios/plugins/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/icinga2 $(1)/usr/sbin/
	$(CP) -r $(PKG_INSTALL_DIR)/usr/share/icinga2/* $(1)/usr/share/icinga2/
endef

define Package/icinga2/conffiles
/usr/var/lib/icinga2/certs
/etc/icinga2
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,$(PKG_NAME)))

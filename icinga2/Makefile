include $(TOPDIR)/rules.mk

PKG_NAME:=icinga2
PKG_VERSION:=2.12.3
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Icinga/icinga2.git
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
	DEPENDS:=+boost-context +boost-coroutine +boost-date_time +boost-filesystem +boost-thread +boost-system +boost-program_options +boost-regex +libopenssl +libatomic +libedit +libncurses
	URL:=https://icinga.com/
	USERID:=icinga2:icinga2
endef

define Package/$(PKG_NAME)/description
	Icinga 2 is a general-purpose monitoring application to fit the needs of any size of network. Icinga 1.x was a Nagios fork; this new generation has been rewritten from scratch in C++, with multi-threading and cluster support.
endef

define Host/Install
	$(INSTALL_DIR) $(STAGING_DIR_HOSTPKG)/bin
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/Bin/Release/mkclass $(STAGING_DIR_HOSTPKG)/bin/
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/Bin/Release/mkembedconfig $(STAGING_DIR_HOSTPKG)/bin/
endef

define Package/$(PKG_NAME)/install
	$(CP) -r $(PKG_INSTALL_DIR)/* $(1)/
	rm -r $(1)/usr/share/doc
	rm -r $(1)/usr/share/man
	rm -r $(1)/etc/bash_completion.d
	rm -r $(1)/etc/init.d
	rm -r $(1)/etc/logrotate.d
	rm -r $(1)/etc/sysconfig
	rm $(1)/usr/lib/icinga2/prepare-dirs $(1)/usr/lib/icinga2/safe-reload
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/icinga2.init $(1)/etc/init.d/icinga2
endef

define Package/icinga2/conffiles
/etc/icinga2/icinga2.conf
/etc/icinga2/zones.conf
/etc/icinga2/constants.conf
/etc/icinga2/scripts/mail-service-notification.sh
/etc/icinga2/scripts/mail-host-notification.sh
/etc/icinga2/conf.d/users.conf
/etc/icinga2/conf.d/timeperiods.conf
/etc/icinga2/conf.d/templates.conf
/etc/icinga2/conf.d/notifications.conf
/etc/icinga2/conf.d/services.conf
/etc/icinga2/conf.d/hosts.conf
/etc/icinga2/conf.d/groups.conf
/etc/icinga2/conf.d/downtimes.conf
/etc/icinga2/conf.d/commands.conf
/etc/icinga2/conf.d/app.conf
/etc/icinga2/features-available/syslog.conf
/etc/icinga2/features-available/mainlog.conf
/etc/icinga2/features-available/debuglog.conf
/etc/icinga2/features-available/api.conf
/etc/icinga2/features-available/icingadb.conf
/etc/icinga2/features-available/perfdata.conf
/etc/icinga2/features-available/opentsdb.conf
/etc/icinga2/features-available/elasticsearch.conf
/etc/icinga2/features-available/influxdb.conf
/etc/icinga2/features-available/graphite.conf
/etc/icinga2/features-available/gelf.conf
/etc/icinga2/features-available/notification.conf
/etc/icinga2/features-available/livestatus.conf
/etc/icinga2/features-available/statusdata.conf
/etc/icinga2/features-available/compatlog.conf
/etc/icinga2/features-available/command.conf
/etc/icinga2/features-available/checker.conf
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,$(PKG_NAME)))

# chown -R icinga2:icinga2 /usr/var/lib/icinga2/
# chown -R icinga2:icinga2 /etc/icinga2

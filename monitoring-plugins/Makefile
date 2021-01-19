include $(TOPDIR)/rules.mk

PKG_NAME:=monitoring-plugins
PKG_VERSION:=2.3
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/monitoring-plugins/monitoring-plugins.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Build/Prepare
	$(Build/Prepare/Default)
	(cd $(PKG_BUILD_DIR) && ./tools/setup)
endef

CONFIGURE_ARGS += \
	--libexecdir=/usr/lib/nagios/plugins \
	--with-openssl=$(STAGING_DIR)/usr \
	--without-dbi \
	--without-ldap \
	--without-mysql \
	--without-pgsql \
	--without-radius \
	--with-ps-command="/bin/ps -w" \
	--with-ps-cols="6" \
	--with-ps-format="%d %s %d %s %s %n" \
	--with-ps-varlist="&procpid$(comma)&procuid$(comma)&procvsz$(comma)procstat$(comma)procprog$(comma)&pos" \
i	--with-ping-command="/usr/bin/ping -n -U -w %d -c %d %s" \
	--with-ping6-command="/usr/bin/ping6 -n -U -w %d -c %d %s" \
	--with-nslookup-command="/usr/bin/nslookup" \
	--with-uptime-command="/usr/bin/uptime" \
	--with-rpcinfo-command="/usr/bin/rpcinfo" \
	--with-smbclient-command="/usr/bin/smbclient" \
	--with-snmpget-command="" \
	--with-snmpgetnext-command="" \
	--with-qstat-command="" \
	--with-fping-command="/usr/bin/fping" \
	--with-fping6-command="/usr/bin/fping" \
	--with-ssh-command="/usr/bin/ssh" \
	--with-sudo-command="" \
	--with-mailq-command="/usr/sbin/mailq" \
	--with-qmail-qstat-command="" \
	--with-proc-meminfo="/proc/meminfo" \
	--with-dig-command="/usr/bin/dig" \
	--with-apt-get-command="" \
	--with-perl="/usr/bin/perl"

define Package/monitoring-plugins
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=monitoring-plugins (native modules)
	DEPENDS:=+libopenssl +libpthread +iputils-ping +iputils-ping6
	URL:=https://www.monitoring-plugins.org/
endef

define Package/monitoring-plugins/description
	Plugins for nagios compatible monitoring systems like Naemon and Icinga.
endef

define Package/monitoring-plugins/install
	$(CP) -r $(PKG_INSTALL_DIR)/* $(1)/
	$(INSTALL_SUID) $(PKG_BUILD_DIR)/plugins-root/check_dhcp $(1)/usr/lib/nagios/plugins/check_dhcp
	$(INSTALL_SUID) $(PKG_BUILD_DIR)/plugins-root/check_icmp $(1)/usr/lib/nagios/plugins/check_icmp
	rm $(1)/usr/lib/nagios/plugins/check_uptime
	rm $(1)/usr/lib/nagios/plugins/check_file_age
	rm $(1)/usr/lib/nagios/plugins/check_mailq
	rm $(1)/usr/lib/nagios/plugins/check_ifoperstatus
	rm $(1)/usr/lib/nagios/plugins/check_ifstatus
	rm $(1)/usr/lib/nagios/plugins/check_wave
	rm $(1)/usr/lib/nagios/plugins/check_rpc
	rm $(1)/usr/lib/nagios/plugins/check_ircd
	rm $(1)/usr/lib/nagios/plugins/check_flexlm
	rm $(1)/usr/lib/nagios/plugins/check_disk_smb
	rm $(1)/usr/lib/nagios/plugins/check_breeze
endef

define Package/monitoring-plugins-perl
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=monitoring-plugins (Perl-based modules)
	DEPENDS:=+perl +perlbase-posix +perlbase-getopt +perlbase-findbin +perlbase-english
	URL:=https://www.monitoring-plugins.org/
endef

define Package/monitoring-plugins-perl/description
	Plugins for nagios compatible monitoring systems like Naemon and Icinga.
endef

define Package/monitoring-plugins-perl/install
	$(INSTALL_DIR) $(1)/usr/lib/nagios/plugins
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_uptime $(1)/usr/lib/nagios/plugins/check_uptime
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_file_age $(1)/usr/lib/nagios/plugins/check_file_age
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_mailq $(1)/usr/lib/nagios/plugins/check_mailq
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_ifoperstatus $(1)/usr/lib/nagios/plugins/check_ifoperstatus
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_ifstatus $(1)/usr/lib/nagios/plugins/check_ifstatus
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_wave $(1)/usr/lib/nagios/plugins/check_wave
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_rpc $(1)/usr/lib/nagios/plugins/check_rpc
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_ircd $(1)/usr/lib/nagios/plugins/check_ircd
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_flexlm $(1)/usr/lib/nagios/plugins/check_flexlm
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_disk_smb $(1)/usr/lib/nagios/plugins/check_disk_smb
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/nagios/plugins/check_breeze $(1)/usr/lib/nagios/plugins/check_breeze
endef

$(eval $(call BuildPackage,monitoring-plugins))
$(eval $(call BuildPackage,monitoring-plugins-perl))

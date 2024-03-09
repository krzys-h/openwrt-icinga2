#
# Copyright (C) 2017 Philip Prindeville <philipp@redfish-solutions.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=perl-net-snmp
PKG_VERSION:=v6.0.1
PKG_RELEASE:=1

PKG_SOURCE_NAME:=Net-SNMP
PKG_SOURCE_URL:=https://cpan.metacpan.org/authors/id/D/DT/DTOWN/
PKG_SOURCE:=$(PKG_SOURCE_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=14c37bc1cbb3f3cdc7d6c13e0f27a859f14cdcfd5ea54a0467a88bc259b0b741

PKG_LICENSE:=GPL-1.0-or-later Artistic-1.0-Perl
PKG_MAINTAINER:=Philip Prindeville <philipp@redfish-solutions.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/perl/$(PKG_SOURCE_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include perlmod.mk

define Package/perl-net-snmp
  SUBMENU:=Perl
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Object oriented interface to SNMP
  URL:=http://search.cpan.org/dist/$(PKG_SOURCE_NAME)/
  DEPENDS:=+perl +perlbase-digest +perlbase-math
endef

define Build/Configure
	$(call perlmod/Configure,,)
endef

define Build/Compile
	$(call perlmod/Compile,,)
endef

define Package/perl-net-snmp/install
	$(call perlmod/Install,$(1),Net)
endef


$(eval $(call BuildPackage,perl-net-snmp))

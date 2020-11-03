#
# Copyright (C) 2009-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mdk3
PKG_VERSION:=v6
PKG_RELEASE:=2
PKG_MD5SUM:=9c605890827334e63123bb18c6715962a9b5973e4eacd3d480cad4059f3bdab1

PKG_BUILD_DIR:=$(BUILD_DIR)/mdk3-master-master
PKG_SOURCE_URL:=https://github.com/charlesxsh/mdk3-master/archive/
PKG_SOURCE:=master.zip

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mdk3
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpthread
  TITLE:= MDK3
  URL:=http://homepages.tu-darmstadt.de/~p_larbig/wlan/
  SUBMENU:=wireless
endef

define Package/mdk3/description
  Tool to exploit wireless vulnerabilities
endef

MAKE_FLAGS += \
	$(TARGET_CONFIGURE_OPTS)

define Package/mdk3/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_BUILD_DIR)/mdk3 $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,mdk3))

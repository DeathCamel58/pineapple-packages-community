#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=geoip-api-c
PKG_VERSION:=1.6.12
PKG_RELEASE:=1

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://api.github.com/repos/maxmind/geoip-api-c/tarball/
PKG_HASH:=49149fd84a02d5e2beafaeca33eb73bc84f9004265f9ab14797f6bc8aea84d4b
PKG_BUILD_DIR:=$(BUILD_DIR)/geoip-api-c-$(PKG_VERSION)

# Fix automake scripts automagically per <https://openwrt.org/docs/guide-developer/packages#pkg_fixup>
PKG_FIXUP:=autoreconf
PKG_FIXUP:=patch-libtool
PKG_FIXUP:=gettext-version

include $(INCLUDE_DIR)/package.mk

define Package/geoip-api-c
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GeoIP Legacy C Library
  URL:=https://github.com/maxmind/geoip-api-c
endef

define Package/geoip-api-c/description
	The GeoIP Legacy C library enables the user to find geographical and network
	information of an IP address.
endef

TARGET_LDFLAGS += $(LIBRPC)

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		LD="$(TARGET_CXX)" \
		all
	$(MAKE) -C $(PKG_BUILD_DIR) \
	    install DESTDIR=$(PKG_INSTALL_DIR)
endef

define Package/geoip-api-c/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libGeoIP.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/geoip.pc $(1)/usr/lib/pkgconfig/
	
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/{geoiplookup,geoiplookup6} $(1)/usr/bin/
	
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/{GeoIP,GeoIPCity}.h $(1)/usr/include/
	    
	$(INSTALL_DIR) $(1)/usr/man/man1
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/man/man1/* $(1)/usr/man/man1/
	
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libGeoIP.so $(STAGING_DIR)/usr/lib/GeoIP.so
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libGeoIP.so.1 $(STAGING_DIR)/usr/lib/GeoIP.so.1
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libGeoIP.so.1.6.12 $(STAGING_DIR)/usr/lib/GeoIP.so.1.6.12
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libGeoIP.a $(STAGING_DIR)/usr/lib/GeoIP.a
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libGeoIP.la $(STAGING_DIR)/usr/lib/GeoIP.la
endef

$(eval $(call BuildPackage,geoip-api-c))

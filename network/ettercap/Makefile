#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ettercap
PKG_VERSION:=0.8.3.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Ettercap/ettercap/releases/download/v$(PKG_VERSION)/
PKG_HASH:=6186e87e320cc12c81fb5cbe47335885a3e51f90681e8b79f34ceae66e99becf

CMAKE_INSTALL:=1

PKG_MAINTAINER:=Dylan Corrales <info@randomcpu.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=geoip-api-c libiconv-full

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/ettercap
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcap +libnet-1.2.x +libopenssl +libpcre +libncurses +libltdl +libpthread +zlib +geoip-api-c +curl +libiconv-full
  TITLE:=Ettercap is a suite for man in the middle attacks on LAN.
  URL:=http://ettercap.sourceforge.net
endef

define Package/ettercap/description
	It features sniffing of live connections, content filtering on the fly
	and many other interesting tricks.
	It supports active and passive dissection of many protocols (even
	ciphered ones) and includes many feature for network and host analysis.
endef

define Package/ettercap/conffiles
    /etc/ettercap/etter.conf
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/lib/libiconv-full/include -liconv
TARGET_LDFLAGS += -L$(STAGING_DIR)/usr/lib/libiconv-full/lib

CMAKE_OPTIONS += -S . -B build \
    -DENABLE_GTK=OFF \
    -DENABLE_IPV6=ON \
    -DINSTALL_DESKTOP=OFF \
    -DENABLE_GEOIP=OFF
    
MAKE_FLAGS += -C build \
	DESTDIR="$(PKG_INSTALL_DIR)"

define Package/ettercap/install
	$(INSTALL_DIR) $(1)/etc/ettercap
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/ettercap/etter.{conf,dns,mdns,nbns} $(1)/etc/ettercap/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/etter{cap,filter,log} $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib/ettercap
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ettercap/*.so $(1)/usr/lib/ettercap/
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/*.so{,.0,.0.8.3.1} $(1)/usr/lib/ettercap/
	$(INSTALL_DIR) $(1)/usr/share/ettercap
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/ettercap/* $(1)/usr/share/ettercap/
endef

$(eval $(call BuildPackage,ettercap))

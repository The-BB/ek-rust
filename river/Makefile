# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

# XXX Atomic{I,U}64

include $(TOPDIR)/rules.mk

PKG_NAME:=river
PKG_VERSION:=0.2.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/memorysafety/river/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=7c3aebe1e60a53d2d80b81db6b074623b7797570a07dfad93c7f6ae8df0f9b37

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE-APACHE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0438

define Package/river
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  TITLE:=a reverse proxy application
  URL:=https://www.memorysafety.org/initiative/reverse-proxy/
  DEPENDS:=@!(mips||mipsel) +libopenssl
endef

define Package/river/description
  river is a Reverse Proxy Application based on the pingora library
  from Cloudflare. 
endef

define Package/river/conffiles
/opt/etc/river/config.toml
endef

CARGO_SOURCE_SUBDIR:=source/river

# error: failed to run custom build command for `openssl-sys v0.9.102`
RUSTC_VARS += OPENSSL_NO_VENDOR=1

define Package/river/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S80river $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/etc/river
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/source/river/assets/test* \
		$(1)/opt/etc/river
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/source/river/assets/test-config.toml \
		$(1)/opt/etc/river/config.toml
	$(SED) 's,\./assets,/opt/etc/river,g' $(1)/opt/etc/river/config.toml
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/river $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,river))

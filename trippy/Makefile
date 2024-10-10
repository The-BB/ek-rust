# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=trippy
PKG_VERSION:=0.11.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/fujiapple852/trippy/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=2745d5b02b32bc9de8944ec9c37f27c5dea4c5dedb2b0a9b969e515f2aafdf84

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0438

define Package/trippy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A network diagnostic tool
  URL:=https://github.com/fujiapple852/trippy
endef

define Package/trippy/description
  A network diagnostic tool, inspired by mtr.
endef

define Package/trippy/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/trip $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,trippy))

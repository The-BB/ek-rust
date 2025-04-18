# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=dysk
PKG_VERSION:=2.10.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/Canop/dysk/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=af6a19493f3ca1d471605cd3e40016aaf89d383c87705f6c32d8232b7e433c14

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

define Package/dysk
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Filesystem
  TITLE:=A linux utility listing your filesystems
  URL:=https://github.com/Canop/dysk
  PROVIDES:=lfs
endef

define Package/dysk/description
  A linux utility to get information on filesystems, like df but better.
endef

define Package/dysk/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/dysk $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,dysk))

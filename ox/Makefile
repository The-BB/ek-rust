# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=ox
PKG_VERSION:=0.6.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/curlpipe/ox/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=410dc77ea2fcb9e73b8cba5121c3cf41215d4cf8cd219015d5f8e0caea4e42d7

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

define Package/ox
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Editors
  TITLE:=A Rust powered text editor
  URL:=https://github.com/curlpipe/ox
endef

define Package/ox/description
  Ox is a code editor that runs in your terminal.
endef

define Package/ox/conffiles
/opt/etc/.oxrc
endef

define Package/ox/install
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/config/.oxrc $(1)/opt/etc
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ox $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,ox))

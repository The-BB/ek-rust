# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=tokei
PKG_VERSION:=13.0.0_alpha5
PKG_VERSION_TAG:=13.0.0-alpha.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION_TAG).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/XAMPPRocky/tokei/tar.gz/refs/tags/v$(PKG_VERSION_TAG)?
PKG_HASH:=03db714caf9fe64adbeef5abd6ba48096b1d63bbd1871aaf5b1fcd9985f8e7d6

PKG_LICENSE:=Apache-2.0 MIT
PKG_LICENSE_FILES:=LICENSE-APACHE LICENSE-MIT

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0438
PKG_UNPACK += --strip-components=1 -C $(PKG_BUILD_DIR)

define Package/tokei
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=count your code, quickly
  URL:=https://tokei.rs
endef

define Package/tokei/description
  Tokei is a program that displays statistics about your code.
  Tokei will show the number of files, total lines within those
  files and code, comments, and blanks grouped by language.
endef

define Package/tokei/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/tokei $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,tokei))

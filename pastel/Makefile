# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=pastel
PKG_VERSION:=0.9.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/sharkdp/pastel/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=473c805de42f6849a4bb14ec103ca007441f355552bdb6ebc80b60dac1f3a95d

PKG_LICENSE:=Apache-2.0 MIT
PKG_LICENSE_FILES:=LICENSE-APACHE LICENSE-MIT

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

define Package/pastel
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Image Manipulation
  TITLE:=a tool to generate, analyze, convert, manipulate colors
  URL:=https://github.com/sharkdp/pastel
  DEPENDS:=@!USE_MUSL
endef

define Package/pastel/description
  A command-line tool to generate, analyze, convert and manipulate
  colors.
endef

define Package/pastel/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/pastel $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,pastel))

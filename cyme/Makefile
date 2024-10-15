# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=cyme
PKG_VERSION:=1.8.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/tuna-f1sh/cyme/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=f3b7f71e52fd29809f25aadff4d949aafe0ff088d514ca587e7103d5b4171d5b

PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0438 udevrs-030

define Package/cyme
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=List system USB buses and devices
  URL:=https://github.com/tuna-f1sh/cyme
  DEPENDS:=+libusb-1.0 @!USE_MUSL
endef

define Package/cyme/description
  List system USB buses and devices; a lib and modern cross-platform
  lsusb that attempts to maintain compatibility with, but also add new features.
endef

define Package/cyme/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cyme $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,cyme))

# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=hck
PKG_VERSION:=0.10.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/sstadick/hck/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=8aecac1a52852f238390e9e20c85b14846d1b6c1035920603d1a8196396896d3

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE-MIT UNLICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

define Package/hck
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=a sharp cut(1) clone
  URL:=https://github.com/sstadick/hck
endef

define Package/hck/description
  hck is a shortening of hack, a rougher form of cut.
endef

ifeq ($(CONFIG_arm),y)
TARGET_CFLAGS += -mfloat-abi=softfp
endif

define Package/hck/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/hck $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,hck))

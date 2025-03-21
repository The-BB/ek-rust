# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

# XXX mips(el) (arti)

include $(TOPDIR)/rules.mk

PKG_NAME:=coarsetime
PKG_VERSION:=0.1.35
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/jedisct1/rust-coarsetime/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=b5393e944d0e5d81d15478f625cfe321d86f3db5c3834ea4fc761d187ac9ae39

PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../../rustc-dev/cargo.mk

PKG_UNPACK += --strip-components=1 -C $(PKG_BUILD_DIR)

define Package/coarsetime-$(PKG_VERSION)
  SECTION:=devel
  CATEGORY:=Development
  SUBMENU:=Libraries
  TITLE:=Time and duration crate optimized for speed
  URL:=https://github.com/jedisct1/rust-coarsetime
  BUILDONLY:=1
endef

define Package/coarsetime-$(PKG_VERSION)/description
  A Rust crate to make time measurements, that focuses on speed.
endef

ifeq ($(or $(CONFIG_mips),$(CONFIG_mipsel)),y)
  define Build/Prepare
	$(Build/Prepare/Default)
	patch -p1 -d $(PKG_BUILD_DIR) < ./patches-32bit/010-fix.patch
  endef
endif

Build/Compile:=:
MoveLibs:=:
Build/InstallDev:=:

$(eval $(call BuildPackage,coarsetime-$(PKG_VERSION)))

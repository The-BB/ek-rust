# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=cpumap
PKG_VERSION:=0.2.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://codeberg.org/Kiith/cpumap
PKG_MIRROR_HASH:=1113e6018394a1febc0dd4278fa306292cdd0800a1c0e84d1312682380a2b5e8

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

define Package/cpumap
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=CPU tools
  TITLE:=view and edit CPU affinities
  URL:=https://codeberg.org/Kiith/cpumap
  DEPENDS:=@!(mips||mipsel) +libhwloc
endef

define Package/cpumap/description
  CPUMap is a graphical (TUI and GUI) tool to view and edit CPU
  affinity of processes on a Linux system.
endef

define Package/cpumap/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cpumap $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,cpumap))

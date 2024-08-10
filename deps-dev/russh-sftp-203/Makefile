# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

# XXX mips(el) (hex-patch)

include $(TOPDIR)/rules.mk

PKG_NAME:=russh-sftp
PKG_VERSION:=2.0.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=951aa3c8594031a72c8a26858f342b07a3e2abbd
PKG_SOURCE_URL:=https://github.com/AspectUnk/russh-sftp
PKG_MIRROR_HASH:=b627d4543a04b84ad6be798e09911146fce3bf46be786dbe4dc474d59659a4f5

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0438 flurry-051 seize-033

define Package/russh-sftp-$(PKG_VERSION)
  SECTION:=devel
  CATEGORY:=Development
  SUBMENU:=Libraries
  TITLE:=SFTP subsystem supported server and client for Russh
  URL:=https://github.com/AspectUnk/russh-sftp
  BUILDONLY:=1
endef

define Package/russh-sftp-$(PKG_VERSION)/description
  SFTP subsystem supported server and client for Russh and more!
endef

Build/Compile:=:
MoveLibs:=:
Build/InstallDev:=:

$(eval $(call BuildPackage,russh-sftp-$(PKG_VERSION)))

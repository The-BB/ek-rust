# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=yvers
PKG_REAL_VERSION:=0.0.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2023-06-12
PKG_SOURCE_VERSION:=5e6e49d43e94975182453cb6e3af77bd6aa63325
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_DATE).tar.zst
PKG_SOURCE_URL:=https://github.com/TokieSan/yvers
PKG_MIRROR_HASH:=1c4666259bce8c23864643fbacdd23800f7f5139feef9a80fd38c668f7472a4d

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0431

define Package/yvers
  SECTION:=admin
  CATEGORY:=Administration
  TITLE:=An extensible TUI system monitor
  URL:=https://github.com/TokieSan/yvers
endef

define Package/yvers/description
  Yvers is a new extensible TUI system monitor and a Linux Process
  Manager based on ytop with numerous improvements and the addition of the
  capability to dynamically add widgets created by the community.
endef

define Package/yvers/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/yvers $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,yvers))

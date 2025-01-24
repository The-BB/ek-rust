# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=fish-shell
PKG_REAL_VERSION:=4.0.0-beta.1
PKG_VERSION:=$(subst -beta.,_beta,$(PKG_REAL_VERSION))
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=4.0b1
PKG_SOURCE_URL:=https://github.com/fish-shell/fish-shell
PKG_MIRROR_HASH:=7a076af6348e9a70fd485bd6e98ceb348e723b5c42104e95d8522edaa463c384

PKG_LICENSE:=GPL-2.0-only LGPL-2.0-or-later MIT PSF-2.0
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Entware team, https://entware.net

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../rustc-dev/cargo.mk

define Package/fish-shell
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=the friendly interactive shell
  URL:=https://fishshell.com/
  DEPENDS:=+libpcre2 +libpcre2-32
  CONFLICTS:=fish
endef

define Package/fish-shell/description
  The user-friendly command line shell.
endef

RUSTC_VARS += \
	PREFIX=/opt \
	BINDIR=/opt/usr/bin \
	DATADIR=/opt/share \
	DOCDIR=/opt/share/doc \
	LOCALEDIR=/opt/share/locale \
	SYSCONFDIR=/opt/etc \
	FISH_BUILD_DOCS=0 \
	FISH_BUILD_VERSION=$(PKG_REAL_VERSION)

define FixPaths
	$(SED) 's,@STAGING_DIR@,$(STAGING_DIR),g' $(PKG_BUILD_DIR)/build.rs
endef
Hooks/Compile/Pre += FixPaths

define Package/fish-shell/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/fish $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/fish_indent $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/fish_key_reader $(1)/opt/usr/bin
endef

define Package/fish-shell/postinst
#!/bin/sh

[ -d "/opt/share/fish" ] || fish --install -vn > /dev/null 2>&1
endef

$(eval $(call BuildPackage,fish-shell))

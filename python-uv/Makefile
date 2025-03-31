# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=uv
PKG_VERSION:=0.6.10
PKG_RELEASE:=1

PYPI_NAME:=uv
PKG_HASH:=cbbb03deb30af457cd93ad299ee5c3258ade3d900b4dee1af936c8a6d87d5bcb

PKG_LICENSE:=Apache-2.0 MIT
PKG_LICENSE_FILES:=LICENSE-APACHE LICENSE-MIT

PKG_BUILD_DEPENDS:=boxcar-027 getrandom-0215 maturin/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-uv
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=An extremely fast Python package and project manager
  URL:=https://pypi.org/project/uv/
  DEPENDS:= \
	+python3-asyncio \
	+python3-ctypes \
	+python3-logging \
	+python3-setuptools \
	+python3-urllib
  EXTRA_DEPENDS:=maturin
endef

RUSTFLAGS += -C relocation-model=pic

define Package/python3-uv/description
  An extremely fast Python package and project manager, written in Rust.
endef

define Package/python3-uv/postrm
#!/bin/sh

rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)
rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)-$(PKG_VERSION).dist-info
endef

$(eval $(call Py3Package,python3-uv))
$(eval $(call BuildPackage,python3-uv))
#$(eval $(call BuildPackage,python3-uv-src))

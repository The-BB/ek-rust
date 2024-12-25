# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=cryptography
PKG_VERSION:=43.0.1
PKG_RELEASE:=1

PYPI_NAME:=cryptography
PKG_HASH:=203e92a75716d8cfb491dc47c79e17d0d9207ccffcbcb35f598fbe463ae3444d

PKG_LICENSE:=Apache-2.0 BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE LICENSE.APACHE LICENSE.BSD LICENSE.PSF
PKG_MAINTAINER:=Entware team, https://entware.net

PKG_BUILD_DEPENDS:= \
	libffi/host \
	python-cffi/host \
	python-setuptools-rust/host \
	python-wheel/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-cryptography
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Cryptographic recipes and primitives (rust)
  URL:=https://github.com/pyca/cryptography
  DEPENDS:= \
	+libopenssl \
	+libopenssl-legacy \
	+python3-cffi \
	+python3-distutils \
	+python3-email \
	+python3-urllib \
	+python3-uuid
endef

define Package/python3-cryptography/description
  cryptography is a package which provides cryptographic recipes and primitives
  to Python developers. Our goal is for it to be your "cryptographic standard
  library". It supports Python 3.6+ and PyPy3 7.2+.
endef

RUSTFLAGS += -C relocation-model=pic

TARGET_CPPFLAGS += -I$(PYTHON3_INC_DIR)

define Package/python3-cryptography/postrm
#!/bin/sh

rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)
rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)-$(PKG_VERSION).dist-info
endef

$(eval $(call Py3Package,python3-cryptography))
$(eval $(call BuildPackage,python3-cryptography))
#$(eval $(call BuildPackage,python3-cryptography-src))

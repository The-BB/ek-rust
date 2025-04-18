# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=suricata-update
PKG_VERSION:=1.3.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/OISF/suricata-update/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=5aa3b07a078d793c8e4cdd54b9022e0fe024ade7522d5ddc3167449279490f9c

PKG_BUILD_DIR:=$(BUILD_DIR)/pypi/$(PKG_NAME)-$(PKG_VERSION)

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=python-yaml/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/suricata-update
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Suricata Update Tool (python)
  URL:=https://github.com/OISF/suricata-update
  DEPENDS:= \
	+python3-dateutil \
	+python3-logging \
	+python3-openssl \
	+python3-urllib \
	+python3-yaml
endef

define Package/suricata-update/description
  The tool for updating your Suricata rules.
endef

define Package/suricata-update/postrm
#!/bin/sh

rm -rf $(PYTHON3_PKG_DIR)/suricata
rm -rf $(PYTHON3_PKG_DIR)/suricata_update-$(PKG_VERSION).dist-info
endef

$(eval $(call Py3Package,suricata-update))
$(eval $(call BuildPackage,suricata-update))
#$(eval $(call BuildPackage,suricata-update-src))

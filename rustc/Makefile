# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=rustc
PKG_VERSION:=1.86.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-src.tar.gz
PKG_SOURCE_URL:=https://static.rust-lang.org/dist
PKG_HASH:=022a27286df67900a044d227d9db69d4732ec3d833e4ffc259c4425ed71eed80

PKG_LICENSE:=Apache-2.0 MIT
PKG_LICENSE_FILES:=LICENSE-APACHE LICENSE-MIT

PKG_BUILD_DEPENDS:=libiconv-full rustc-dev

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

PKG_UNPACK += --strip-components=1 -C $(PKG_BUILD_DIR)

define Package/rustc
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=Rust
  URL:=https://www.rust-lang.org
  DEPENDS:=+libatomic +libcurl +libopenssl +libstdcpp +zlib
  EXTRA_DEPENDS:=gcc
endef

define Package/rustc/description
  The Rust Programming Language.
endef

define Package/rustc/conffiles
/opt/etc/profile.d/
/opt/share/cargo/config.toml
endef

### host
HOST_PKG_CONFIG_PATH:="$(STAGING_DIR_HOST)/lib/pkgconfig:$(STAGING_DIR_HOSTPKG)/lib/pkgconfig"

### target
ifeq ($(CONFIG_TARGET_armv7_3_2),y)
  RUSTC_TARGET_ARCH:=$(subst arm,armv7,$(REAL_GNU_TARGET_NAME))
else
  RUSTC_TARGET_ARCH:=$(REAL_GNU_TARGET_NAME)
endif

define Build/Configure
	( \
		echo 'change-id = 139182'; \
		echo '[llvm]'; \
		echo 'download-ci-llvm = false'; \
		echo 'allow-old-toolchain = true'; \
		echo 'targets = "AArch64;ARM;Mips;X86"'; \
		echo 'experimental-targets = ""'; \
		echo 'cflags = "-pthread"'; \
		echo 'cxxflags = "-pthread"'; \
		echo 'ldflags = "-lz -latomic -lpthread -ldl"'; \
		echo 'link-shared = false'; \
		echo 'build-config = \
		{ \
			LLVM_ENABLE_BINDINGS="OFF", \
			LLVM_ENABLE_OCAMLDOC="OFF", \
			LLVM_INCLUDE_BENCHMARKS="OFF", \
			LLVM_INCLUDE_DOCS="OFF", \
			LLVM_INCLUDE_EXAMPLES="OFF", \
			LLVM_INCLUDE_RUNTIMES="OFF", \
			LLVM_INCLUDE_TESTS="OFF", \
			LLVM_INCLUDE_TOOLS="ON", \
			LLVM_INCLUDE_UTILS="OFF" \
		}'; \
		echo '[build]'; \
		echo 'host = ["$(RUSTC_TARGET_ARCH)"]'; \
		echo 'target = ["$(RUSTC_TARGET_ARCH)"]'; \
		echo 'bootstrap-cache-path = "$(DL_DIR)/rustc"'; \
		echo 'cargo = "$(STAGING_DIR)/host/bin/cargo"'; \
		echo 'cargo-clippy = "$(STAGING_DIR)/host/bin/cargo-clippy"'; \
		echo 'python = "$(STAGING_DIR_HOST)/bin/python3"'; \
		echo 'rustc = "$(STAGING_DIR)/host/bin/rustc"'; \
		echo 'rustfmt = "$(STAGING_DIR)/host/bin/rustfmt"'; \
		echo 'compiler-docs = false'; \
		echo 'docs = false'; \
		echo 'extended = true'; \
		echo 'full-bootstrap = false'; \
		echo 'local-rebuild = false'; \
		echo 'submodules = false'; \
		echo 'tools = ["cargo", "clippy", "rustdoc", "rustfmt",]'; \
		echo 'vendor = true'; \
		echo 'verbose = $(if $(findstring s,$(OPENWRT_VERBOSE)),1,0)'; \
		echo '[install]'; \
		echo 'prefix = "/opt"'; \
		echo 'sysconfdir = "/opt/etc"'; \
		echo 'bindir = "/opt/bin"'; \
		echo 'libdir = "/opt/lib"'; \
		echo 'datadir = "/opt/share"'; \
		echo '[rust]'; \
		$(if $(CONFIG_USE_MUSL),echo 'musl-root = "$(TOOLCHAIN_DIR)"'; ) \
		echo 'channel = "nightly"'; \
		echo 'codegen-tests = false'; \
		echo 'dist-src = false'; \
		echo 'download-rustc = false'; \
		echo 'incremental = false'; \
		echo 'rpath = true'; \
		echo '[target.$(RUSTC_TARGET_ARCH)]'; \
		echo 'ar = "$(TARGET_CROSS)ar"'; \
		echo 'cc = "$(TARGET_CROSS)gcc"'; \
		echo 'cxx = "$(TARGET_CROSS)g++"'; \
		echo 'linker = "$(TARGET_CROSS)gcc"'; \
		echo 'ranlib = "$(TARGET_CROSS)ranlib"'; \
		$(if $(CONFIG_USE_MUSL),echo 'crt-static = false'; ) \
		echo '[dist]'; \
		echo 'src-tarball = false'; \
		echo 'compression-formats = ["gz"]'; \
	) > $(PKG_BUILD_DIR)/config.toml

	$(FIND) $(PKG_BUILD_DIR)/vendor -type f -name ".cargo-checksum.json" -exec \
		$(SED) 's/\("files":{\)[^}]*/\1/' {} +
endef

define Build/Compile
	( cd $(PKG_BUILD_DIR); \
		CARGO_HOME="$(STAGING_DIR)/host/share/cargo.dev" \
		DESTDIR=$(PKG_INSTALL_DIR) \
		HOST_PKG_CONFIG_PATH="$(HOST_PKG_CONFIG_PATH)" \
		PKG_CONFIG_ALLOW_CROSS=1 \
		$(STAGING_DIR_HOST)/bin/python3 x.py install; \
	)
endef

Build/Install:=:

define Package/rustc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cargo{,-clippy,-fmt} $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/clippy-driver $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/rust{c,doc,fmt} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/profile.d
	$(INSTALL_DATA) ./files/cargo.sh $(1)/opt/etc/profile.d
	$(INSTALL_DIR) $(1)/opt/lib/rustlib/$(RUSTC_TARGET_ARCH)
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib*.so $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/rustlib/$(RUSTC_TARGET_ARCH)/lib \
		$(1)/opt/lib/rustlib/$(RUSTC_TARGET_ARCH)
	$(INSTALL_DIR) $(1)/opt/share/cargo
	$(INSTALL_DATA) ./files/config.toml $(1)/opt/share/cargo
	$(SED) 's,@RUSTC_TARGET_ARCH@,$(RUSTC_TARGET_ARCH),; \
		s,@TARGET_CC@,$(TARGET_CC),' \
			$(1)/opt/share/cargo/config.toml
endef

$(eval $(call BuildPackage,rustc))

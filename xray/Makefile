include $(TOPDIR)/rules.mk

PKG_NAME:=xray
PKG_VERSION:=1.1.1
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  TITLE:=A platform for building proxies
  URL:=https://https://github.com/XTLS/Xray-core
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Project V
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-certificates
endef


define Package/$(PKG_NAME)/description
Project V is a set of network tools that help you to build your own computer network.
It secures your network connections and thus protects your privacy.

  This package contains xray.
endef

# 禁止OpenWrt对二进制文件进行strip
STRIP:=true

ifeq ($(ARCH),i386)
	PKG_ARCH_XRAY:=32
endif

ifeq ($(ARCH),x86_64)
	PKG_ARCH_XRAY:=64
endif

ifeq ($(ARCH),mipsel)
	PKG_ARCH_XRAY:=mips64
endif

ifeq ($(ARCH),mips)
	PKG_ARCH_XRAY:=mips32
endif

ifeq ($(ARCH),arm)
ifeq ($(BOARD),bcm53xx)
	PKG_ARCH_XRAY:=arm32-v5
else ifeq ($(BOARD),kirkwood)
	PKG_ARCH_XRAY:=arm32-v5
else
	PKG_ARCH_XRAY:=arm32-v7a
endif
endif

ifeq ($(ARCH),aarch64)
	PKG_ARCH_XRAY:=arm64-v8a
endif


PKG_SOURCE:=Xray-linux-${PKG_ARCH_XRAY}.zip

PKG_SOURCE_URL:=https://github.com/XTLS/Xray-core/releases/download/v${PKG_VERSION}

UNZIP_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_NAME)-unzip

PKG_HASH:=skip

define Build/Prepare
	mkdir -vp $(UNZIP_DIR)
	unzip -od $(UNZIP_DIR) $(DL_DIR)/$(PKG_SOURCE)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin/xray
	chmod +x $(UNZIP_DIR)/xray
	$(STAGING_DIR_HOST)/bin/upx --lzma --best $(UNZIP_DIR)/xray || true
	$(INSTALL_BIN) $(UNZIP_DIR)/xray $(1)/usr/bin/xray/xray
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

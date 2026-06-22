include $(TOPDIR)/rules.mk

PKG_NAME:=chirpstack-gateway-utils
PKG_VERSION:=0.1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/chirpstack/chirpstack-gateway-utils/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=edc3adbcb2bed897190093d0d6a460a1dca9ef71b9c5de599f8502ae28b83aa9

PKG_MAINTAINER:=Orne Brocaar <info@brocaar.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=rust/host

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/rust/rust-package.mk

define Package/chirpstack-gateway-utils
	SECTION:=chirpstack
	CATEGORY:=ChirpStack
	TITLE:=ChirpStack Gateway Utils
	URL:=https://github.com/chirpstack/chirpstack-gateway-utils
	DEPENDS:=+luci-app-statistics +collectd-mod-exec
endef

define Package/chirpstack-gateway-utils/description
	ChirpStack Gateway Utils
endef

define Package/chirpstack-gateway-utils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/* $(1)/usr/bin

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/etc/uci-defaults/90-configure-chirpstack-gateway-utils $(1)/etc/uci-defaults

	$(INSTALL_DIR) $(1)/www/luci-static/resources/statistics/rrdtool/definitions
	$(INSTALL_DATA) ./files/www/luci-static/resources/statistics/rrdtool/definitions/battery.js $(1)/www/luci-static/resources/statistics/rrdtool/definitions
endef

define Build/Compile
	$(call Build/Compile/Cargo)
endef

$(eval $(call RustBinPackage,chirpstack-gateway-utils))
$(eval $(call BuildPackage,chirpstack-gateway-utils))

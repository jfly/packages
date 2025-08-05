include $(TOPDIR)/rules.mk

PKG_NAME:=wifi-presence
PKG_VERSION:=issue-30-workaround
PKG_RELEASE:=1
BRANCH:=issue-30-workaround

PKG_SOURCE:=-wifi-presence-$(BRANCH).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/jfly/wifi-presence/tar.gz/$(BRANCH)?
PKG_HASH:=99867b2c4a49982732c60893b88b015ee5451a0bb8e2e466c44a5df2d6a1e59c

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Adam Williams <pwnfactory@gmail.com>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/awilliams/wifi-presence
GO_PKG_BUILD_PKG:=$(GO_PKG)/cmd/wifi-presence

include $(INCLUDE_DIR)/package.mk
include ../../lang/golang/golang-package.mk

define Package/wifi-presence
  SECTION:=net
  CATEGORY:=Network
  TITLE:=WiFi presence detection with Home Assistant integration
  URL:=https://github.com/awilliams/wifi-presence
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/wifi-presence/description
  WiFi presence detection with Home Assistant integration.
  Publish WiFi client connect and disconnect events to MQTT.
endef

define Package/wifi-presence/conffiles
/etc/config/wifi-presence
endef

define Package/wifi-presence/install
	$(call GoPackage/Package/Install/Bin,$(PKG_INSTALL_DIR))

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/wifi-presence $(1)/usr/bin

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/wifi-presence.conf $(1)/etc/config/wifi-presence

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/wifi-presence.init $(1)/etc/init.d/wifi-presence
endef

$(eval $(call GoBinPackage,wifi-presence))
$(eval $(call BuildPackage,wifi-presence))

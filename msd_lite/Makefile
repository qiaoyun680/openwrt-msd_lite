include $(TOPDIR)/rules.mk

PKG_NAME:=msd_lite
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/rozhuk-im/msd_lite.git
PKG_SOURCE_DATE:=2024-04-29
PKG_SOURCE_VERSION:=db583386ca47d803e44d9adc98b1ec6a4abb5d9a

PKG_MAINTAINER:=Your Name <your.email@example.com>
PKG_LICENSE:=BSD-2-Clause

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk


define Package/msd_lite
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Convert UDP IPTV streams into HTTP streams
	URL:=https://github.com/rozhuk-im/msd_lite
endef

define Package/msd_lite/description
	Convert UDP IPTV streams into HTTP streams
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(foreach PATCH,$(wildcard $(PKG_BUILD_DIR)/patches/*.patch), \
		$(PATCH) -p1 < $(PATCH) || exit 1; )
endef

define Package/msd_lite/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/msd_lite $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/msd_lite

	$(INSTALL_CONF) ./files/msd_lite.conf.sample $(1)/etc/msd_lite/msd_lite.conf

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/msd_lite.init $(1)/etc/init.d/msd_lite

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/msd_lite.conf $(1)/etc/config/msd_lite
endef


$(eval $(call BuildPackage,msd_lite))
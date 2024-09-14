include $(TOPDIR)/rules.mk

PKG_NAME:=msd_lite
PKG_VERSION:=master
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/rozhuk-im/msd_lite.git
PKG_SOURCE_VERSION:=master

PKG_MAINTAINER:=Your Name <your.email@example.com>
PKG_LICENSE:=BSD-2-Clause

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

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
	# 可以在这里进行源码的额外操作，例如打补丁
	cp -r $(DL_DIR)/msd_lite $(PKG_BUILD_DIR)

endef

define Build/Compile
	# 使用 OpenWrt 的默认编译方式，通常会调用 make
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/msd_lite/install
	# 安装二进制文件到 /usr/sbin
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/msd_lite $(1)/usr/sbin/

	# 安装默认配置文件
	$(INSTALL_DIR) $(1)/etc/msd_lite
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/etc/msd_lite/msd_lite.conf.sample $(1)/etc/msd_lite/msd_lite.conf

	# 安装 init.d 脚本
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/msd_lite.init $(1)/etc/init.d/msd_lite

	# 安装 UCI 配置文件
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/msd_lite.conf $(1)/etc/config/msd_lite
endef

$(eval $(call BuildPackage,msd_lite))

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-clash
PKG_VERSION:=0.21.0
PKG_RELEASE:=1
PKG_MAINTAINER:=frainzy1477


include $(INCLUDE_DIR)/package.mk

define Package/luci-app-clash
	SECTION:=luci
	CATEGORY:=LuCI
	SUBMENU:=2. Services
	TITLE:=LuCI app for clash
	DEPENDS:=+bash +coreutils-nohup +wget
	PKGARCH:=all
	MAINTAINER:=frainzy1477
endef

define Package/luci-app-clash/description
	LuCI configuration for clash.
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
rm -rf /tmp/luci*
/etc/init.d/clash disable
endef

define Build/Prepare
	${CURDIR}/tools/po2lmo/src/po2lmo ${CURDIR}/po/zh-cn/clash.po ${CURDIR}/po/zh-cn/clash.zh-cn.lmo
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi/clash
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view/clash
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/clash
	$(INSTALL_DIR) $(1)/www
	$(INSTALL_DIR) $(1)/usr/share/clash
	$(INSTALL_DIR) $(1)/usr/share/clash/web
	$(INSTALL_DIR) $(1)/usr/share/clash/dashboard
	$(INSTALL_DIR) $(1)/usr/share/clash/dashboard/img
	$(INSTALL_DIR) $(1)/usr/share/clash/dashboard/js

	$(INSTALL_BIN) 	./root/etc/init.d/clash $(1)/etc/init.d/clash
	$(INSTALL_CONF) ./root/etc/config/clash $(1)/etc/config/clash
	$(INSTALL_CONF) ./root/etc/clash/* $(1)/etc/clash/

	$(INSTALL_BIN) ./root/usr/share/clash/clash-watchdog.sh $(1)/usr/share/clash/
	$(INSTALL_BIN) ./root/usr/share/clash/clash.sh $(1)/usr/share/clash/
	$(INSTALL_BIN) ./root/usr/share/clash/ipdb.sh $(1)/usr/share/clash/
	$(INSTALL_BIN) ./root/usr/share/clash/dns.yml $(1)/usr/share/clash/
	$(INSTALL_BIN) ./root/usr/share/clash/clash_version $(1)/usr/share/clash/
	$(INSTALL_BIN) ./root/usr/share/clash/check_version.sh $(1)/usr/share/clash/
	
	$(INSTALL_BIN) ./root/usr/share/clash/web/* $(1)/usr/share/clash/web
	$(INSTALL_BIN) ./root/usr/share/clash/dashboard/index.html $(1)/usr/share/clash/dashboard/
	$(INSTALL_BIN) ./root/usr/share/clash/dashboard/main.5b2a02b81ea75793d649.css $(1)/usr/share/clash/dashboard/
	$(INSTALL_BIN) ./root/usr/share/clash/dashboard/img/33343e6117c37aaef8886179007ba6b5.png $(1)/usr/share/clash/dashboard/img/
	$(INSTALL_BIN) ./root/usr/share/clash/dashboard/img/logo.png $(1)/www/
	$(INSTALL_BIN) ./root/usr/share/clash/dashboard/js/* $(1)/usr/share/clash/dashboard/js/
        
	$(INSTALL_DATA) ./luasrc/controller/*.lua $(1)/usr/lib/lua/luci/controller/
	$(INSTALL_DATA) ./luasrc/model/cbi/clash/*.lua $(1)/usr/lib/lua/luci/model/cbi/clash/
	$(INSTALL_DATA) ./luasrc/view/clash/* $(1)/usr/lib/lua/luci/view/clash/
	$(INSTALL_DATA) ./po/zh-cn/clash.zh-cn.lmo $(1)/usr/lib/lua/luci/i18n/
	
endef

$(eval $(call BuildPackage,luci-app-clash))

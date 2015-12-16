include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-berlin-meta
PKG_VERSION:=0.0.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-berlin-meta/Default
  SECTION:=freifunk-berlin
  CATEGORY:=freifunk-berlin
  TITLE:=Freifunk Berlin meta-package
  URL:=http://github.com/freifunk-berlin/packages_berlin
#  DEPENDS+= +hostapd
endef

define Package/freifunk-berlin-meta/Default/description
  Freifunk Berlin meta-package for basic dependencies
endef

COMMON_MINIMAL=+libiwinfo-lua \
            +luci-theme-bootstrap +uhttpd-mod-ubus +freifunk-berlin-uhttpd-defaults \
            +luci-app-ffwizard-berlin +community-profiles \
            +freifunk-berlin-dhcp-defaults +freifunk-berlin-firewall-defaults +freifunk-berlin-network-defaults \
            +freifunk-berlin-migration \
            +freifunk-berlin-olsrd-defaults +olsrd-mod-arprefresh +olsrd-mod-dyn-gw +luci-app-olsr-services \
            +olsrd-mod-jsoninfo +olsrd-mod-nameservice \
            +freifunk-berlin-openvpn-files +openvpn-polarssl \
            +dnsmasq +qos-scripts \
            +luci-app-owm +luci-app-owm-cmd \
            +freifunk-berlin-freifunk-defaults

define Package/freifunk-berlin-meta-default4MB
$(call Package/freifunk-berlin-meta/Default)
  TITLE+= (FF-Node 4MB-Flash)
  DEPENDS+= +wpad $(COMMON_MINIMAL)
endef

define Package/freifunk-berlin-meta-default4MB/description
$(call Package/freifunk-berlin-meta/Default/description)
  Freifunk Berlin default router with only 4MB flash
endef

define Package/freifunk-berlin-meta-default
$(call Package/freifunk-berlin-meta/Default)
  TITLE+= (FF-Node)
  DEPENDS+= $(COMMON_MINIMAL) +hostapd \
            +olsrd-mod-txtinfo +olsrd-mod-watchdog \
            +freifunk-watchdog \
            +freifunk-berlin-statistics-defaults +luci-i18n-statistics-de \
            +collectd-mod-interface +collectd-mod-iwinfo +collectd-mod-network +collectd-mod-olsrd \
            +collectd-mod-rrdtool +collectd-mod-ping +collectd-mod-uptime +collectd-mod-memory \
            +batctl +alfred
endef

define Package/freifunk-berlin-meta-default/description
$(call Package/freifunk-berlin-meta/Default/description)
  Freifunk Berlin default router with 8+MB flash
endef

FF_BERLIN_DIR=$(PKG_BUILD_DIR)/files/freifunk-berlin

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)/files
	git clone https://github.com/freifunk-berlin/firmware.git $(FF_BERLIN_DIR)
endef

define Build/Compile
	cp $(TOPDIR)/package/base-files/files/etc/banner $(PKG_BUILD_DIR)/files
	patch -d $(PKG_BUILD_DIR)/files -p5 < $(FF_BERLIN_DIR)/patches/002-banner-info.patch
endef

define Package/freifunk-berlin-meta-default4MB/install
	true
#	$(INSTALL_DIR) $(1)/etc/uci-defaults
#	$(CP) ./uci-defaults/* $(1)/etc/uci-defaults
endef

define Package/freifunk-berlin-meta-default/install
	true
#	$(INSTALL_DIR) $(1)/etc/uci-defaults
#	$(CP) ./uci-defaults/* $(1)/etc/uci-defaults
endef

$(eval $(call BuildPackage,freifunk-berlin-meta-default))
$(eval $(call BuildPackage,freifunk-berlin-meta-default4MB))

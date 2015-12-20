include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-berlin-meta
PKG_VERSION:=0.0.0
PKG_RELEASE:=2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-berlin-meta/Default
  SECTION:=freifunk-berlin
  CATEGORY:=freifunk-berlin
  TITLE:=Freifunk Berlin meta-package
  URL:=http://github.com/freifunk-berlin/packages_berlin
  PKG_BUILD_DEPENDS:=+base-files
endef

define Package/freifunk-berlin-meta/Default/description
  Freifunk Berlin meta-package for basic dependencies
endef

COMMON_MINIMAL=+dnsmasq \
            +freifunk-common +community-profiles \
            +freifunk-berlin-dhcp-defaults +freifunk-berlin-freifunk-defaults \
            +freifunk-berlin-network-defaults +freifunk-berlin-olsrd-defaults \
            +luci-app-ffwizard-berlin \
            +luci-app-olsr-services +olsrd-mod-arprefresh +olsrd-mod-dyn-gw +kmod-ipip \
            +luci-app-owm +luci-app-owm-cmd \
            +libiwinfo-lua +iwinfo \
            +luci-theme-bootstrap \
            +qos-scripts 

DEFAULT_ROUTER=+freifunk-berlin-firewall-defaults +freifunk-berlin-migration \
            +iptables-mod-filter \
            +uboot-envtools \
            +uhttpd +uhttpd-mod-ubus


define Package/freifunk-berlin-meta-default4MB
$(call Package/freifunk-berlin-meta/Default)
  TITLE+= (FF-Node 4MB-Flash)
  DEPENDS:= $(COMMON_MINIMAL) $(DEFAULT_ROUTER) +wpad-mini
endef

define Package/freifunk-berlin-meta-default4MB/description
$(call Package/freifunk-berlin-meta/Default/description)
  Freifunk Berlin default router with only 4MB flash
endef

define Package/freifunk-berlin-meta-default
$(call Package/freifunk-berlin-meta/Default)
  TITLE+= (FF-Node)
  DEPENDS:= $(COMMON_MINIMAL) +hostapd \
            +olsrd-mod-txtinfo +olsrd-mod-watchdog \
            +freifunk-berlin-statistics-defaults +freifunk-berlin-uhttpd-defaults \
            +freifunk-watchdog \
            +luci-i18n-statistics-de \
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
	# use original Freifunk-Berlin patch to build new banner-text
	cp $(TOPDIR)/package/base-files/files/etc/banner $(PKG_BUILD_DIR)/files
	patch -d $(PKG_BUILD_DIR)/files -p5 < $(FF_BERLIN_DIR)/patches/002-banner-info.patch
	echo  >$(PKG_BUILD_DIR)/files/change_banner "#!/bin/sh"
	echo >>$(PKG_BUILD_DIR)/files/change_banner "cat >/etc/banner <<BANNER_TEXT"
	cat  >>$(PKG_BUILD_DIR)/files/change_banner $(PKG_BUILD_DIR)/files/banner
	echo >>$(PKG_BUILD_DIR)/files/change_banner "BANNER_TEXT"
endef

define Package/freifunk-berlin-meta-default4MB/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(CP) $(PKG_BUILD_DIR)/files/change_banner $(1)/etc/uci-defaults
endef

define Package/freifunk-berlin-meta-default/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(CP) $(PKG_BUILD_DIR)/files/change_banner $(1)/etc/uci-defaults
endef

#define Package/freifunk-berlin-meta-default4MB/postint
##!/bin/sh 
#if [ -z $${IPKG_INSTROOT} ] ; then
#    ( . /etc/uci-defaults/change_banner ) && rm -f /etc/uci-defaults/change_banner
#fi
#endef

#define Package/freifunk-berlin-meta-default/postint
##!/bin/sh 
#if [ -z $${IPKG_INSTROOT} ] ; then
#    ( . /etc/uci-defaults/change_banner ) && rm -f /etc/uci-defaults/change_banner
#fi
#endef

$(eval $(call BuildPackage,freifunk-berlin-meta-default))
$(eval $(call BuildPackage,freifunk-berlin-meta-default4MB))

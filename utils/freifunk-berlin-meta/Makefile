include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-berlin-meta
PKG_VERSION:=0.0.1
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-berlin-meta/Default
  SECTION:=freifunk-berlin
  CATEGORY:=freifunk-berlin
  TITLE:=Freifunk Berlin meta packages
  URL:=http://github.com/freifunk-berlin/packages_berlin
  DEPENDS+= +hostapd
endef

define Package/freifunk-berlin-meta/description/Default
  Freifunk Berlin configuration files for firewall
endef

define Package/freifunk-berlin-meta-default4MB
$(call Package/freifunk-berlin-meta/Default)
  TITLE+= (default4MB)
  DEPENDS:= +wpad \
            +luci-app-ffwizard-berlin \
            +freifunk-berlin-openvpn-files \
            +freifunk-berlin-olsrd-defaults +olsrd-mod-arprefresh +olsrd-mod-dyn-gw \
            +olsrd-mod-jsoninfo +olsrd-mod-nameservice
endef

define Package/freifunk-berlin-meta-default4MB/description
$(call Package/freifunk-berlin-meta/description/Default)
  Freifunk Berlin default router with only 4MB flash
endef

define Package/freifunk-berlin-meta-default
$(call Package/freifunk-berlin-meta/Default)
  TITLE+= (default)
  DEPENDS:= +freifunk-berlin-meta-default4MB \
            +olsrd-mod-txtinfo +olsrd-mod-watchdog \
            +freifunk-watchdog \
            +freifunk-berlin-statistics-defaults
endef

define Package/freifunk-berlin-meta-default/description
$(call Package/freifunk-berlin-meta/description/Default)
  This meta-package contains only dependencies for a minimal IKEv2 setup.
  Freifunk Berlin default router
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

#define Package/freifunk-berlin-firewall-defaults/install
#	$(INSTALL_DIR) $(1)/etc/uci-defaults
#	$(CP) ./uci-defaults/* $(1)/etc/uci-defaults
#endef

$(eval $(call BuildPackage,freifunk-berlin-meta-default))
$(eval $(call BuildPackage,freifunk-berlin-meta-default4MB))

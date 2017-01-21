# $Id: Makefile 2010-02-04 23:25:21Z pg $

include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-berlin-vpn03-files
PKG_VERSION:=0.0.3
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-berlin-vpn03-files
  SECTION:=freifunk-berlin
  CATEGORY:=freifunk-berlin
  TITLE:=Freifunk Berlin VPN03 files
  URL:=http://github.com/freifunk-berlin/packages_berlin
  DEPENDS+= @(PACKAGE_openvpn-polarssl||PACKAGE_openvpn-mbedtls) +freifunk-berlin-lib-guard
  PKGARCH:=all
endef

define Package/freifunk-berlin-vpn03_openvpn-files/description
  Freifunk Berlin openVPN files
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/freifunk-berlin-vpn03_openvpn-files/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(CP) ./uci-defaults/* $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/etc/openvpn
	$(CP) ./files/freifunk-ca.crt $(1)/etc/openvpn
	$(INSTALL_DIR) $(1)/lib/freifunk
	$(CP) ./openvpn/ffvpn-up.sh $(1)/lib/freifunk
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(CP) ./openvpn/60-ffopenvpn $(1)/etc/hotplug.d/iface
endef

$(eval $(call BuildPackage,freifunk-berlin-vpn03_openvpn-files))

# $Id: Makefile 2010-02-04 23:25:21Z pg $

include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-berlin-vpn03-files
PKG_VERSION:=0.0.3
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-berlin-vpn03-files/default
  SECTION:=freifunk-berlin
  CATEGORY:=freifunk-berlin
  URL:=http://github.com/freifunk-berlin/packages_berlin
  DEPENDS+= +freifunk-berlin-lib-guard
  PKGARCH:=all
endef

define Package/freifunk-berlin-vpn03_openvpn-files
  $(call Package/freifunk-berlin-vpn03-files/default)
  TITLE:=Freifunk Berlin VPN03 files (OpenVPN)
  DEPENDS:=+openvpn-x509
endef

define Package/freifunk-berlin-vpn03_openvpn-files/description
  Freifunk Berlin openVPN files
endef

define Package/freifunk-berlin-vpn03_ipsec-files
  $(call Package/freifunk-berlin-vpn03-files/default)
  TITLE:=Freifunk Berlin VPN03 files (IpSec)
  DEPENDS:=+strongswan-minimal +strongswan-mod-pem +strongswan-mod-openssl +vtiv4 +vti
endef

define Package/freifunk-berlin-vpn03_ipsec-files/description
  Freifunk VPN03 files for IpSec-tunnels
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

define Package/freifunk-berlin-vpn03_ipsec-files/install
	$(INSTALL_DIR) $(1)/etc/ipsec.d/cacerts
	$(CP) ./files/freifunk-ca.crt $(1)/etc/ipsec.d/cacerts/
endef

$(eval $(call BuildPackage,freifunk-berlin-vpn03_openvpn-files))
$(eval $(call BuildPackage,freifunk-berlin-vpn03_ipsec-files))

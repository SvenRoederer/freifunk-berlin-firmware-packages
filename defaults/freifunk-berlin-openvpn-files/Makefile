include $(TOPDIR)/rules.mk

LUCI_TITLE:=Freifunk Berlin openVPN files (commmon)
LUCI_DEPENDS:=+openvpn +freifunk-berlin-lib-guard +freifunk-berlin-network-defaults
LUCI_DESCRIPTION:=Freifunk Berlin openVPN files

define Package/freifunk-berlin-openvpn-defaults/postinst
# noop
endef

include ../../freifunk-berlin-generic.mk

# call BuildPackage - is done via freifunk-berlin-generic.mk --> luci.mk

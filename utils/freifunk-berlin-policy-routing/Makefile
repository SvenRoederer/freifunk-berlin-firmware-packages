include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-berlin-policy-routing
PKG_VERSION:=0.0.1
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-berlin-policy-routing
  SECTION:=freifunk-berlin
  CATEGORY:=freifunk-berlin
  TITLE:=Freifunk Berlin policy-routing script
  URL:=http://github.com/freifunk-berlin/packages_berlin
  PKGARCH:=all
endef

define Package/freifunk-berlin-policy-routing/description
  Freifunk Berlin policy-routing script, with probably some
  advantages to the original freifunk-policy-routing of LuCI
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/freifunk-berlin-policy-routing/install
	$(CP) ./files/hotplug.d/* $(1)/etc/hotplug.d/
endef

$(eval $(call BuildPackage,freifunk-berlin-policy-routing))

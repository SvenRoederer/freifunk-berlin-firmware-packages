include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-berlin-freifunk-defaults
PKG_VERSION:=0.0.2
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-berlin-freifunk-defaults
  SECTION:=freifunk-berlin
  CATEGORY:=freifunk-berlin
  TITLE:=Freifunk Berlin freifunk default configuration
  URL:=http://github.com/freifunk-berlin/packages_berlin
endef

define Package/freifunk-berlin-freifunk-defaults/description
  Freifunk Berlin configuration files for freifunk
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
	mkdir -p $(PKG_BUILD_DIR)/files
	echo  >$(PKG_BUILD_DIR)/files/freifunk-berlin "#!/bin/sh"
	echo >>$(PKG_BUILD_DIR)/files/freifunk_berlin "cat >/etc/config/freifunk <<OVERWRITE_TEXT"
	cat  >>$(PKG_BUILD_DIR)/files/freifunk_berlin ./files/etc/config/freifunk
	echo >>$(PKG_BUILD_DIR)/files/freifunk_berlin "OVERWRITE_TEXT"
endef

define Build/Compile
endef

define Package/freifunk-berlin-freifunk-defaults/install
	$(INSTALL_DIR) $(1)/etc/uci_defaults
	$(CP) $(PKG_BUILD_DIR)/files/freifunk_berlin $(1)/etc/uci_defaults/
endef

$(eval $(call BuildPackage,freifunk-berlin-freifunk-defaults))

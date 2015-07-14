include $(TOPDIR)/rules.mk

PKG_NAME:=nodewatcher
PKG_VERSION:=1.0.0
PKG_VERSION:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/nodewatcher
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Nodewatcher: client component for Netmon
  DEPENDS:=+uhttpd
endef

define Package/nodewatcher/description
	Freifunk Oldenburg Nodewatcher used to provide status data for Netmon
endef

define Build/Prepare
	echo "all: " > $(PKG_BUILD_DIR)/Makefile
endef

define Package/nodewatcher/install
	$(CP) ./files/* $(1)/
	chmod +x $(1)/usr/sbin/nodewatcher
	chmod +x $(1)/usr/sbin/configurator
	mkdir -p $(1)/lib/cron
	echo "# netmon" >> $(1)/lib/cron/${PKG_NAME}
	echo "*/5 * * * * /usr/sbin/nodewatcher; /usr/sbin/configurator" >> $(1)/lib/cron/${PKG_NAME}
	mkdir -p $(1)/www/public
	ln -s ../../tmp/node.data $(1)/www/public/node.data
endef

$(eval $(call BuildPackage,nodewatcher))

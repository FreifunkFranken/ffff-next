include $(TOPDIR)/rules.mk

PKG_NAME:=fastdstart
PKG_VERSION:=1.0.0
PKG_VERSION:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/fastdstart
  SECTION:=net
  CATEGORY:=Network
  TITLE:=fastd key exchange
  DEPENDS:=+fastd
endef

define Package/fastdstart/description
	Simple script to exchange fastd keys and start fastd
endef

define Build/Prepare
	echo "all: " > $(PKG_BUILD_DIR)/Makefile
endef

define Package/fastdstart/install
	$(CP) ./files/* $(1)/
	chmod +x $(1)/usr/sbin/fastdstart
	mkdir -p $(1)/lib/cron
	echo "#check for new vpn keys every 5 mins" >> $(1)/lib/cron/${PKG_NAME}
	echo "*/5 * * * * /usr/sbin/fastdstart" >> $(1)/lib/cron/${PKG_NAME}
endef

$(eval $(call BuildPackage,fastdstart))

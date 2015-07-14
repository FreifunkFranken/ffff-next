include $(TOPDIR)/rules.mk

PKG_NAME:=freifunk-franken
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/freifunk

include $(INCLUDE_DIR)/package.mk

define Package/freifunk-franken-basic
	SECTION:=base
	CATEGORY:=Config
	DEFAULT:=n
	TITLE:= Freifunk-Franken Basic
	URL:=http://freifunk-franken.de
	DEPENDS:=+kmod-batman-adv     \
	         +batctl              \
	         +alfred              \
	         +fastd               \
	         +fastdstart          \
	         +ip                  \
	         +odhcpd              \
	         +dnsmasq-dhcpv6      \
	         +ebtables            \
	         +kmod-ebtables-ipv4  \
	         +kmod-ebtables-ipv6  \
	         +haveged             \
	         +@ATH_USER_REGD      \
	         +nodewatcher
endef

define Build/Prepare
	echo "all: " > $(PKG_BUILD_DIR)/Makefile
endef

define Package/freifunk-franken-basic/install
	$(CP) ./files/* $(1)/
	mkdir -p $(1)/lib/cron
	echo "#reboot every 1 days at 04:05" >> $(1)/lib/cron/$(PKG_NAME)
	echo "1 4 */5 * * /sbin/reboot" >> $(1)/lib/cron/$(PKG_NAME)
endef

define Package/freifunk-franken/conffiles
	/etc/config/freifunk
endef

define Package/freifunk-franken-debug
	SECTION:=base
	CATEGORY:=Config
	DEFAULT:=n
	TITLE:=Freifunk-Franken with debug tools
	DEPENDS:=+freifunk-franken-basic     \
	         +@KMOD_BATMAN_ADV_DEBUG_LOG \
	         +iperf                      \
	         +tcpdump-mini
endef

$(eval $(call BuildPackage,freifunk-franken-basic))
$(eval $(call BuildPackage,freifunk-franken-debug))

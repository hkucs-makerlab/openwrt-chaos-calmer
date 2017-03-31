#
include $(TOPDIR)/rules.mk

PKG_NAME:=ipvsadm
PKG_VERSION:=1.26

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.linuxvirtualserver.org/software/kernel-2.6/
PKG_MD5SUM:=eac3ba3f62cd4dea2da353aeddd353a8

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

ifeq ($(CONFIG_DEVEL),y)
	export QUILT=1
endif

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=IP Virtual Server Configuration Manager
	URL:=http://www.linuxvirtualserver.org
	DEPENDS:= +kmod-ipvs +libnl-tiny +libpopt
endef

#    -I$(STAGING_DIR)/usr/include/libnl/linux -fPIC -DLIBIPVS_USE_NL
TARGET_CFLAGS += \
    -I$(STAGING_DIR)/usr/include/libnl-tiny -fPIC -DLIBIPVS_USE_NL -D_GNU_SOURCE

MAKE_FLAGS += \
	CC="$(TOOLCHAIN_DIR)/bin/$(TARGET_CC)" \
	CXX="$(TOOLCHAIN_DIR)/bin/$(TARGET_CXX)" \
	CFLAGS="$(TARGET_CFLAGS)" \
	LIBS="-lnl-tiny -lpopt"

define Build/Compile
	$(call Build/Compile/Default)
endef

define Package/ipvsadm/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ipvsadm $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ipvsadm-save $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ipvsadm-restore $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

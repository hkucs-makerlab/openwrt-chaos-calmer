#
# Copyright (C) 2008-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=soft-pwm
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define KernelPackage/soft-pwm
	SUBMENU:=Other modules
	TITLE:= Kernel module for soft PWM 
	FILES:= $(PKG_BUILD_DIR)/soft_pwm.ko 
  	AUTOLOAD:=$(call AutoProbe,soft_pwm)
endef

define KernelPackage/soft-pwm/description
	Kernel module for soft PWM 
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		ARCH="$(LINUX_KARCH)" \
		SUBDIRS="$(PKG_BUILD_DIR)" \
		EXTRA_CFLAGS="$(BUILDFLAGS)" \
		modules
endef

$(eval $(call KernelPackage,soft-pwm))


#
# Drivers Copyright (C) 2022 Intel Corporation
#
# This is free software, licensed under the GNU General Public License v2.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=kmod-igb-intel
PKG_VERSION:=5.13.7
PKG_RELEASE:=4

PKG_SOURCE:=igb-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://downloads.sourceforge.net/project/e1000/igb%20stable/$(PKG_VERSION)/
PKG_MD5SUM:=bc7f40d6dcd9c1ac550d265b9dc3aa8d

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

PKG_UNPACK:=zcat $(DL_DIR)/$(PKG_SOURCE) | $(TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf -

define KernelPackage/igb-intel
  SUBMENU:=Network Devices
  TITLE:=Intel igb drivers - oot version from Intel
  DEPENDS:=+kmod-ptp @PCI_SUPPORT
  CONFLICTS:=kmod-igb
  KCONFIG:=CONFIG_IGB \
    CONFIG_IGB_HWMON=n \
    CONFIG_IGB_DCA=n
  FILES:=$(PKG_BUILD_DIR)/src/igb.ko
  AUTOLOAD:=$(call AutoLoad,35,igb)
endef

define Build/Compile
	+$(KERNEL_MAKE) M=$(PKG_BUILD_DIR)/src modules
endef

define KernelPackage/igb-intel/description
 Kernel modules for Intel igb out of tree drivers
endef

$(eval $(call KernelPackage,igb-intel))

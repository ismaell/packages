include $(TOPDIR)/rules.mk

PKG_NAME:=cifsd
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cifsd-team/cifsd.git
PKG_SOURCE_DATE:=2019-07-12
PKG_SOURCE_VERSION:=f2cfe8cb40493a5f77144543bc486bfdb8aa61e2
PKG_MIRROR_HASH:=fd6a3bec5953fa30b87a6e12e2c6666844ad66096afa7de421689f5769626a36

PKG_MAINTAINER:=Andy Walsh <andy.walsh44+github@gmail.com>
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/fs-cifsd
	SUBMENU:=Filesystems
	TITLE:=CIFS/SMB kernel server support
	URL:=https://github.com/cifsd-team/cifsd
	FILES:=$(PKG_BUILD_DIR)/cifsd.ko
	DEPENDS:= \
		+kmod-nls-base \
		+kmod-nls-utf8 \
		+kmod-crypto-md4 \
		+kmod-crypto-md5 \
		+kmod-crypto-hmac \
		+kmod-crypto-ecb \
		+kmod-crypto-des \
		+kmod-crypto-sha256 \
		+kmod-crypto-cmac \
		+kmod-crypto-sha512 \
		+kmod-crypto-aead \
		+kmod-crypto-ccm
endef

define KernelPackage/fs-cifsd/description
	Kernel module for a CIFS/SMBv2,3 fileserver.
endef

# broken atm (needs CONFIG_KEYS=y)
#EXTRA_CFLAGS+=-DCONFIG_CIFSD_ACL

define Build/Compile
	$(KERNEL_MAKE) SUBDIRS="$(PKG_BUILD_DIR)" \
	EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
	CONFIG_CIFS_SERVER=m \
	modules
endef

$(eval $(call KernelPackage,fs-cifsd))

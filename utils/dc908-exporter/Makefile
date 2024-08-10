# SPDX-License-Identifier: GPL-2.0-only
#
# OpenMetrics exporter for Huawei DC908 using gNMI dialout

include $(TOPDIR)/rules.mk

PKG_NAME:=dc908-exporter
PKG_VERSION:=0.9.4
PKG_RELEASE:=1
PKG_SOURCE:=dc908_exporter-v0.9.4-1-g4354523.tar.gz

NODE_ARCH:=$(subst x86_64,amd64,$(ARCH))
PKG_BUILD_DIR=$(BUILD_DIR)/dc908_exporter-$(PKG_VERSION).linux-$(NODE_ARCH)/dist
PKG_SOURCE_URL:=https://github.com/sonix-network/dc908_exporter/releases/download/v$(PKG_VERSION)
PKG_SOURCE_VERSION:=0
PKG_SOURCE_DATE:=2024-07-28
PKG_HASH:=49c240513d55a47a4f570a272fc73cf6fd315f58c2d1663dbdb0843d4acae655

include $(INCLUDE_DIR)/package.mk

define Package/dc908-exporter
  SECTION:=base
  CATEGORY:=Utilities
  TITLE:=Huawei DC908 Prometheus Exporter
  URL:=https://github.com/sonix-network/dc908_exporter
endef

define Package/dc908-exporter/description
  Simple collector designed to take the gNMI dialout stream from one or more
  Huawei OptiXtrans DC908 and export the real-time updates as native Prometheus metrics.
  Prometheus exporter for hardware and OS metrics exposed by *NIX kernels,
  written in Go with pluggable metric collectors.
endef

define Build/Compile
	# Nothing to do
endef

define Package/dc908-exporter/install
	mkdir -p $(1)/etc/init.d/ $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/../dc908_exporter.linux.$(NODE_ARCH) $(1)/usr/bin/dc908_exporter
	chmod +x $(1)/usr/bin/dc908_exporter
	$(CP) ./files/dc908-exporter.init $(1)/etc/init.d/dc908-exporter
	chmod +x $(1)/etc/init.d/dc908-exporter
endef

$(eval $(call BuildPackage,dc908-exporter))

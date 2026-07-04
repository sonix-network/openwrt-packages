# SPDX-License-Identifier: GPL-2.0-only
#
# unwedge - remote control plane for Cisco vEdge 1000 kernel/OS development.
# Prebuilt Go binaries are pulled from the upstream GitHub release, matching the
# convention used by the other Go packages in this feed (dc908-exporter,
# prometheus-node-exporter).

include $(TOPDIR)/rules.mk

PKG_NAME:=unwedge
PKG_VERSION:=0.8.1
PKG_RELEASE:=1

NODE_ARCH:=$(subst x86_64,amd64,$(ARCH))
PKG_BUILD_DIR=$(BUILD_DIR)/unwedge-$(PKG_VERSION)-linux-$(NODE_ARCH)
PKG_SOURCE:=unwedge-$(PKG_VERSION)-linux-$(NODE_ARCH).tar.gz
PKG_SOURCE_URL:=https://github.com/sonix-network/unwedge/releases/download/v$(PKG_VERSION)
PKG_SOURCE_VERSION:=0
PKG_SOURCE_DATE:=2026-07-04
PKG_HASH_mips64:=347d3ad5e9ce48635457206e3f1e10c7922a255122300187be0d6310e3a9dcc7
PKG_HASH_amd64:=eb264aa4d5c5a295fb813163a06c8d978bc57006334cb7013287cf43a771328d
PKG_HASH_arm64:=1d3db71acae9c148dbf017b66be531bc630201e6251f98ccabbe35289732ef9a
PKG_HASH:=$(PKG_HASH_$(NODE_ARCH))

PKG_MAINTAINER:=SONIX <blue@cmd.nu>
PKG_LICENSE:=Apache-2.0

include $(INCLUDE_DIR)/package.mk

define Package/unwedge
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Remote control plane for vEdge 1000 kernel/OS development
  URL:=https://github.com/sonix-network/unwedge
endef

define Package/unwedge/description
  unwedge runs on a controller (itself a Cisco vEdge 1000) and drives a target
  vEdge 1000 for kernel/OS development: it owns the target's serial console,
  power (APC PDU over SNMP), U-Boot interrupt and TFTP netboot, and SSH, and
  exposes them as a gRPC/TLS API. Installs the daemon (unwedged) and the CLI
  (unwedge). Configure /etc/unwedge/config.yaml and enable the service.
endef

define Package/unwedge/conffiles
/etc/unwedge/config.yaml
endef

define Build/Compile
	# Prebuilt release binaries; nothing to compile.
endef

define Package/unwedge/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc/init.d $(1)/etc/unwedge
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/unwedged $(1)/usr/bin/unwedged
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/unwedge $(1)/usr/bin/unwedge
	$(INSTALL_BIN) ./files/unwedge.init $(1)/etc/init.d/unwedge
	$(INSTALL_CONF) ./files/config.yaml $(1)/etc/unwedge/config.yaml
endef

$(eval $(call BuildPackage,unwedge))

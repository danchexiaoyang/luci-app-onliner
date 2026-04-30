# Copyright (C) 2016 Openwrt.org
include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-onliner
PKG_VERSION:=1.0
PKG_RELEASE:=1

LUCI_TITLE:=LuCI support for arp-onliner
LUCI_PKGARCH:=all
# 确保依赖项包含 arp-scan 或其他实现 ARP 扫描的底层工具
LUCI_DEPENDS:=+arp-scan

include $(TOPDIR)/feeds/luci/luci.mk

# 移除手写的 install 区块，让 luci.mk 自动处理 ./luasrc 和 ./root
# 25.12 强烈建议通过标准的 BuildPackage 调用来触发自动化逻辑

define Package/luci-app-onliner/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
    rm -f /tmp/luci-indexcache
    rm -rf /tmp/luci-modulecache/*
    [ -d /usr/share/onliner ] && chmod -R 755 /usr/share/onliner
fi
exit 0
endef

$(eval $(call BuildPackage,luci-app-onliner))

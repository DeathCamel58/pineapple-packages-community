# WiFi Pineapple Community Packages for MK7
*This specific fork is being maintained by DeathCamel57.*

This repository contains the OpenWrt packages for the WiFi Pineapple community repository. Packages found inside this
repository will be available to download to a WiFi Pineapple via opkg.

To make the MK7 pull my precompiled packages, append the line below to `/etc/opkg/customfeeds.conf`.

```
src/gz deathcamel57_19.07_pineapplecommunity https://repo.randomcpu.com/packages/mipsel_24kc/pineapplecommunity
```

I've also decided to compile many, many more of the packages from OpenWRT upstream. Those can be added to OPKG by adding
the below code to the end of `/etc/opkg/customfeeds.conf` (or just a line if you want a specific feed).

```
# DeathCamel57's custom repos
src/gz deathcamel57_19.07_base https://repo.randomcpu.com/packages/mipsel_24kc/base
src/gz deathcamel57_19.07_luci https://repo.randomcpu.com/packages/mipsel_24kc/luci
src/gz deathcamel57_19.07_packages https://repo.randomcpu.com/packages/mipsel_24kc/packages
src/gz deathcamel57_19.07_pineapplecommunity https://repo.randomcpu.com/packages/mipsel_24kc/pineapplecommunity
src/gz deathcamel57_19.07_routing https://repo.randomcpu.com/packages/mipsel_24kc/routing
src/gz deathcamel57_19.07_telephone https://repo.randomcpu.com/packages/mipsel_24kc/telephony
```
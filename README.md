# rpi-lte-proxy

A proxy running on an LTE hat for raspberry pis

# Hardware setup

To get this to work I used the Waveshare SIM7600G-H-PCIE with a 4G/3G LTE Hat with a PCIe slot, this was then hooked up to a Pi 4 (Pi 5 is overkill as the bandwidth of the connection will be the biggest bottleneck in the system). Parts:

- Waveshare SIM7600G-H-PCIE: [https://www.amazon.co.uk/dp/B09LV1VY4S?ref=ppx_yo2ov_dt_b_fed_asin_title](https://www.amazon.co.uk/dp/B09LV1VY4S?ref=ppx_yo2ov_dt_b_fed_asin_title)
- Hat: [https://www.amazon.co.uk/dp/B08TMKCBV7?ref=ppx_yo2ov_dt_b_fed_asin_title](https://www.amazon.co.uk/dp/B08TMKCBV7?ref=ppx_yo2ov_dt_b_fed_asin_title)
- A Sim card with cellular data (no calls/texts needed)

This is basically plug and play but you will need to do some config to make sure that the proxy IP remains static. The connection shows up on the Pi as usb0, you need to make that IP static. To do that I dumped the following config into:

`/etc/network/interfaces.d/usb0`

```text
auto usb0
iface usb0 inet static
  address 192.168.225.10
  netmask 255.255.255.0
  gateway 192.168.225.1
  dns-nameservers 192.168.225.1 8.8.8.8
```

The nameservers (excluding 8.8.8.8), and gateway was derived from the settings defined by the Waveshare device when it created the network interface on the Pi. You can see the default settings by running `ifconfig`.

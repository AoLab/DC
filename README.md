# DC :wrench:
## Introduction
Aolab datacenter is located in Amirkabir CEIT datacenter. Following table describe the configuration of it.

| Host | IP | Users | Remote SSH Access | vCPUs | RAM | Name |
|:----:|:--:|:----- | :------------ | :----: | :---: | :---: |
| platform-base | 172.23.132.37 | parham | 50006 | 6 | 16GB | base.platform.site |
| platform-networking | 172.23.132.51 | parham | - | 4 | 8GB | ns.platform.site |
| platform-kube | 172.23.132.52 | parham | - | 8 | 24GB | kube.platform.site |
| platform-dev-1 | 172.23.132.50 | parham | - | 8 | 8GB | dev1.platform.site |
| platform-dev-2 | 172.23.132.41 | parham | - | 8 | 8GB | dev2.platform.site |

The following URLs are assigned to Aolab:

- [platform, *.platform].ceit.aut.ac.ir --> 172.23.132.37
- backback.ceit.aut.ac.ir

And the following port mapping is avaiable for `platform.ceit.aut.ac.ir`:

- 50008 -> 8000

Platform DNS is available on `platform-networking` and its configuration is available in `coredns`.
In order to use specific dns with dhcp on Ubuntu 18.04, check [this](https://askubuntu.com/questions/1001241/can-netplan-configured-nameservers-supersede-not-merge-with-the-dhcp-nameserve) stackoverflow question or use [this](https://medium.com/@niktrix/getting-rid-of-systemd-resolved-consuming-port-53-605f0234f32f) medium post to handle it forever.

## OpenVPN

In the `platform-base` there is a useful openvpn service with simple configuration that operates on port 8000.
For better usage please use the following command in `ovpn` file:

```
# redirect-gateway def1
route 172.23.0.0 255.255.0.0
```

By this command, only your CEIT traffic will redirect over OpenVPN.
OpenVPN configuration is available under `openvpn` folder for user `parham`. This configuration
needs a key (hint: _somewhere is the best_).

## I1820 Domain

To support `https` we use [Certbot](https://certbot.eff.org) on Ubuntu 18.04.
Please note that we use dns challenge with the following command:

```sh
brew install letsencrypt
sudo certbot certonly --manual -d '*.platform.i1820.org' -d 'platform.i1820.org' --preferred-challenges dns
```

I1820 monitoring is based on [uptime robot](https://uptimerobot.com).

## DNS
- Domain: i1820.org
- Registered with: [Iranserver](https://iranserver.com)
- Managed on: [ArvanCloud](https://npanel.arvancloud.com)

## Aolab Domain

## DNS
- Domain: aolab.org
- Registered with: [Iranserver](https://iranserver.com)
- Managed on: [ArvanCloud](https://npanel.arvancloud.com)

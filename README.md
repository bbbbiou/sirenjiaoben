# XRayR
[本项目源自](https://github.com/XrayR-project/XrayR-release) 此处仅作备份！感谢大神。

## 升级机器

```markdown
yum update -y
yum install -y curl vim wget unzip git nano

```
## 同步时间

```markdown
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

```

## 关闭防火墙

```markdown
systemctl disable firewalld
systemctl stop firewalld

```

## 安装BBR

```markdown
yum install wget
wget -N --no-check-certificate "https://github.000060000.xyz/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

```

>执行`reboot`重新启动

```markdown
./tcp.sh

```


## 安装 Docker/Docker-compose


```markdown
curl -fsSL https://get.docker.com | bash
curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod a+x /usr/local/bin/docker-compose
rm -f `which dc`
ln -s /usr/local/bin/docker-compose /usr/bin/dc

systemctl start docker
service docker start
systemctl enable docker.service
systemctl status docker.service

```

## Docker-compose 安装XrayR

```markdown
yum install -y git
git clone https://github.com/bbbbiou/sirenjiaoben.git && cd sirenjiaoben

```
编辑配置文件：`config.yml`，详见：[配置文件说明](/xrayr-project/xrayr-pei-zhi-wen-jian-shuo-ming/config)
    
## 启动docker

```markdown
docker-compose up -d

```

## 更新XrayR

docker-compose仅需两条简单通用的命令即可实现更新、删除容器并重启。更新软件后config.yml不会被更新覆盖。
注意在 docker-compose.yml 所在的目录下执行：

```markdown
docker-compose pull
docker-compose up -d

```

## 编辑config.yml

```markdown
  -
    PanelType: "V2board" # Panel type: SSpanel, V2board, PMpanel, , Proxypanel
    ApiConfig:
      ApiHost: "https://dingyue.xiuling.buzz"
      ApiKey: "3KKUS2CS7C5Z9YGK"
      NodeID: 2
      NodeType: V2ray # Node type: V2ray, Shadowsocks, Trojan, Shadowsocks-Plugin
      Timeout: 30 # Timeout for the api request
      EnableVless: false # Enable Vless for V2ray Type
      EnableXTLS: false # Enable XTLS for V2ray and Trojan
      SpeedLimit: 0 # Mbps, Local settings will replace remote settings, 0 means disable
      DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
      RuleListPath: # ./rulelist Path to local rulelist file
    ControllerConfig:
      ListenIP: 0.0.0.0 # IP address you want to listen
      SendIP: 0.0.0.0 # IP address you want to send pacakage
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      EnableDNS: false # Use custom DNS config, Please ensure that you set the dns.json well
      DNSType: AsIs # AsIs, UseIP, UseIPv4, UseIPv6, DNS strategy
      EnableProxyProtocol: false # Only works for WebSocket and TCP
      EnableFallback: false # Only support for Trojan and Vless
      FallBackConfigs:  # Support multiple fallbacks
        -
          SNI: # TLS SNI(Server Name Indication), Empty for any
          Path: # HTTP PATH, Empty for any
          Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
          ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
      CertConfig:
        CertMode: dns # Option about how to get certificate: none, file, http, dns. Choose "none" will forcedly disable the tls config.
        CertDomain: "node1.test.com" # Domain to cert
        CertFile: ./cert/node1.test.com.cert # Provided if the CertMode is file
        KeyFile: ./cert/node1.test.com.key
        Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
        Email: test@me.com
        DNSEnv: # DNS ENV option used by DNS provider
          ALICLOUD_ACCESS_KEY: aaa
          ALICLOUD_SECRET_KEY: bbb
```

## DNS提供商参考

dns提供商，所有支持的dns提供商请在此获取：[点击前往](https://go-acme.github.io/lego/dns)


## 付费支持
联系邮箱 [chenfengcloud@gmail.com](mailto:chenfengcloud@gmail.com) 

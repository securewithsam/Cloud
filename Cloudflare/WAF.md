### Cloudflare Best practices 

1# Allow only from Canada
![image](https://github.com/securewithsam/Cloud/assets/85324643/491ddd35-2920-4c18-9ceb-5a9b509322a6)



2# Rate Limiting 
![image](https://github.com/securewithsam/Cloud/assets/85324643/587f2184-e59f-4e58-832f-3c025cfa959a)
![image](https://github.com/securewithsam/Cloud/assets/85324643/fc24fd7b-3104-48a9-9ff1-f11ff2ae816a)
![image](https://github.com/securewithsam/Cloud/assets/85324643/156a0842-480e-4e12-be65-7d4a7ea12869)




3# Custom Rules
![image](https://github.com/securewithsam/Cloud/assets/85324643/bf01a910-c605-44cb-9a58-c65e3f5bcfed)
![image](https://github.com/securewithsam/Cloud/assets/85324643/96d1ac72-5616-4b76-b60e-037b733f2d3f)
![image](https://github.com/securewithsam/Cloud/assets/85324643/63569b67-4d53-4d50-b3d1-295bcaa52128)
![image](https://github.com/securewithsam/Cloud/assets/85324643/82dac27e-dcf0-4166-bb50-550758b0fedc)

#### Expression (Custom rules)
```sh
(http.request.version in {"HTTP/1.0" "HTTP/1.1" "HTTP/1.2"} and http.request.uri eq "/contact/" and not http.user_agent contains "Googlebot" and not http.user_agent contains "Bingbot" and not http.user_agent contains "DuckDuckBot" and not http.user_agent contains "facebot" and not http.user_agent contains "Slurp" and not http.user_agent contains "Alexa")
```


#### Block Bots ( Expression) 
```sh
(http.user_agent contains "Yandex") or (http.user_agent contains "muckrack") or (http.user_agent contains "Qwantify") or (http.user_agent contains "Sogou") or (http.user_agent contains "BUbiNG") or (http.user_agent contains "CFNetwork") or (http.user_agent contains "Scrapy") or (http.user_agent contains "SemrushBot") or (http.user_agent contains "AhrefsBot") or (http.user_agent contains "Baiduspider") or (http.user_agent contains "python-requests") or (http.user_agent contains "crawl" and cf.client.bot) or (http.user_agent contains "bot" and not http.user_agent contains "bingbot" and not http.user_agent contains "Google" and not http.user_agent contains "Twitter" and cf.client.bot) or (http.user_agent contains "Spider" and cf.client.bot and http.user_agent contains "ninja" and http.user_agent contains "attackbot" and http.user_agent contains "backdorbot")
```
#### Block Digital Ocean ASN from other countries
#### Bad ASN List - https://github.com/brianhama/bad-asn-list/blob/master/bad-asn-list.csv
![image](https://github.com/securewithsam/Cloud/assets/85324643/53b8019c-4002-49ee-86d0-07f6d30af216)

```sh
(ip.geoip.asnum in {14061 16276 36352 51167 60117 53667 31034 24940 12876 40021 19994 8560 16509}) or (ip.geoip.asnum in {24940 397630 4134} and ip.geoip.country in {"RU" "CN"} and ip.geoip.continent in {"AS" "NA" "OC" "SA"})
```
#### Form and Comment Spam (Expression)
![image](https://github.com/securewithsam/Cloud/assets/85324643/1243b40c-8012-4be8-9ab0-5cf419acb0c8)

```sh
(http.request.uri contains "/wp-admin/admin-ajax.php" and http.request.method eq "POST" and not http.referer contains "yourwebsitehere.com") or (http.request.uri contains "/wp-comments-post.php" and http.request.method eq "POST" and not http.referer contains "yourwebsitehere.com")
```
####  Challenge Comment Spam 
![image](https://github.com/securewithsam/Cloud/assets/85324643/0abad31f-b007-497c-b59d-e5b01da90ddd)




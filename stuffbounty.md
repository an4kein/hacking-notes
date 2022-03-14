```
unzip targets.zip ;rm targets.zip
cat * |httpx |tee all-targets.txt
for i in $(cat all-targets.txt);do echo $i; curl -s $i/composer.json |grep "\"name\": ";done
BOUNTYYYYYYY LOLLL

[https://hackerone.com/reports/231267](https://hackerone.com/reports/231267)
[https://hackerone.com/reports/461598](https://hackerone.com/reports/461598)
[https://hackerone.com/reports/299552](https://hackerone.com/reports/299552)
```

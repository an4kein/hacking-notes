```
unzip targets.zip
rm target.zip
cat * |httpx |tee all-targets.txt
for i in $(cat all-targets.txt);do echo $i; curl -s $i/composer.json |grep "\"name\": ";done
BOUNTYYYYYYY LOLLL
```

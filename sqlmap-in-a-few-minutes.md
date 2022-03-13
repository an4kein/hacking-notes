
ref: https://0xmahmoudjo0.medium.com/how-i-found-multiple-sql-injection-with-ffuf-and-sqlmap-in-a-few-minutes-9c3bb3780e8f

## Enumeration Phase:

`waybackurls https://redacted.org/ | uro | grep ".php" > php-files.txt`

![image](https://user-images.githubusercontent.com/37910997/158051736-c06d205d-2d01-462d-b415-d2876478c4e2.png)

![image](https://user-images.githubusercontent.com/37910997/158051756-67425eaa-82e4-4c06-8cbc-f74e4ae01e25.png)

```
waybackurls => https://github.com/tomnomnom/waybackurls
uro => https://github.com/s0md3v/uro
```

## Getting Parameters:

`cat php-files.txt| grep -i get | sed 's/.*.get//' | sort -u`

![image](https://user-images.githubusercontent.com/37910997/158052135-c2b8525f-4b29-423f-83c0-1ace98f7e9b8.png)

`cut -f1 -d"."`

![image](https://user-images.githubusercontent.com/37910997/158052170-b61c0137-2ca9-4776-bbf5-a8457ee502ef.png)

sed '/[A-Z]\+/\n&/g'

![image](https://user-images.githubusercontent.com/37910997/158052233-fe8f5937-c7a9-4dcf-8501-3f0b6816b099.png)

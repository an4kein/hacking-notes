ffuf -w /usr/share/seclists/Discovery/Web-Content/[list] -u http://host/FUZZ -X GET -recursion -D -e php,json,pdf,doc,docx,xls

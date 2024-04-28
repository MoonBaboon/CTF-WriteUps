# Forensics
## Browsing-history
![49cbd47706077e61ebc47b353d602db3.png](../_resources/49cbd47706077e61ebc47b353d602db3.png)
I used grep to get the flag format which gave the flag immedietly
```
cat zeus-data.json | grep -o 'nicc{[^}]*}'
```
![b6cdb369c7a726425685561159d9f537.png](../_resources/b6cdb369c7a726425685561159d9f537.png)
`nicc{jup1t3R-15-4W350M3}`
# Misc
## Bad-Singing
![639e96c1bc1ad491e826fdab514eee58.png](../_resources/639e96c1bc1ad491e826fdab514eee58.png)

Using a spectrum analyzer we get the flag
![a9464f7314da4e87c246b2ce7d12a22a.png](../_resources/a9464f7314da4e87c246b2ce7d12a22a.png)
`nicc{jump_in}`

## Horsing-Around-at-Troy

![bbe192561632d0b1e22af7bbbad41ffb.png](../_resources/bbe192561632d0b1e22af7bbbad41ffb.png)

With binwalk we can see that there are multiple files in the jpg
![414e0b5c388425d27200b24016b5fdf8.png](../_resources/414e0b5c388425d27200b24016b5fdf8.png)

After we extract them with:
```
binwalk -e totally-innocent-horse.jpg
```

We get 15 more images or so and one of them contains the flag
```
eog greek.png
```
![cc92e5dfcf65abcc62a3e79e7657b7e7.png](../_resources/cc92e5dfcf65abcc62a3e79e7657b7e7.png)

`nicc{7Ro14-ll1pPo2}`

## Labours-of-hercules-1
![dfb3c7f5cd073693c06cae21d634953e.png](../_resources/dfb3c7f5cd073693c06cae21d634953e.png)
Using steghide and putting the phrase as password we extract the `flag.txt`:
```
steghide extract -sf ../hercules.jpg
```
![986d14af77c9cb58a8b56e192d4c37d6.png](../_resources/986d14af77c9cb58a8b56e192d4c37d6.png)
`flag.txt` contains this:
**How many days/months did Hercules have to kill the create picture depicted here?**

`nicc{thirty_days}`

## Strange-Historical-Machine
![f0346d53c1a50d770c7a86a34dcb6265.png](../_resources/f0346d53c1a50d770c7a86a34dcb6265.png)

The image we get is an image of an enigma machine from WWII

![0c5be56d9bbe52d553f318d340cafdce.png](../_resources/0c5be56d9bbe52d553f318d340cafdce.png)
After using binwalk we get the following text:
**H pzyr wuplgj flbo kmiovyiezv bz amiatez, fpc ynnttrhl hzckv lxkoglk eaqfjlsb sbz dolkqjdw kytksjzktz. Dmvyp fcz nbtleutxh pvgc tyrznyelzdn xqrlbxk hjdb lki iyzg. ftye{E0G_MS0L_3J1AGW_N0Q3}**

Using enigma decoder from https://www.dcode.fr/enigma-machine-cipher we get the following plaintext:
**I have always been interested in history, and learning where various theories and machines originated. There are certainly some interesting cyphers from the past. nicc{Y0U_KN0W_3N1GMA_C0D3}**
`nicc{Y0U_KN0W_3N1GMA_C0D3}`

## Labours-of-hercules-2
![36d60c104067bf7d9eee9d32a1a51cb2.png](../_resources/36d60c104067bf7d9eee9d32a1a51cb2.png)
Using steghide we get the following cipher:
![5dd220bc9b685463865b1d05e4f4aa6c.png](../_resources/5dd220bc9b685463865b1d05e4f4aa6c.png)
**Wt o vsor wg qih ctt, hkc acfs gvozz hoys whg dzoqs.**

**Kvoh qfsohs sjsbhiozzm zsor hc hvs rsawgs ct Vsfoqizsg?**

Using dcode.fr's cipher identifier we find out that it is most likely a ROT Cipher
![02fb16a8676dfc984923c74b5d9e0133.png](../_resources/02fb16a8676dfc984923c74b5d9e0133.png)

`nicc{Lernaean_Hydra}`

## Virtual-spring
![543202d438f22f836e419c30e83c23f7.png](../_resources/543202d438f22f836e419c30e83c23f7.png)

After opening the code on chrome we see that the .js code is heavily obfuscated(You are forgiven Daniel :) )
![49e3bd970d06bf2d0e10965bcd235600.png](../_resources/49e3bd970d06bf2d0e10965bcd235600.png)

After analyzing the code basically there are many functions wiht the name [a-z0-9]

I dont believe my solution is the most intuitive but basically I did put breakpoints on every function and used the debugger to note down what functions were called in order

After debugging it we get the following:
**thespringbouncesuncontrollably**
`nicc{thespringbouncesuncontrollably}`
# Breath-of-the-wild
## Description

![124bf0f76e6ed6e190ac51c1bb3a03c2.png](../_resources/124bf0f76e6ed6e190ac51c1bb3a03c2.png)

## Solution

We get disk image file requested to do some forensic analysis on it. First we determine the type of this image file:

![038a4ca44566de6308a15c32995a7960.png](../_resources/038a4ca44566de6308a15c32995a7960.png)

It seems like it is a `.vhdx` image file so lets add the extension name(so windows can interpret it) and mount to see what is in it:

![9f0aa2b9ff1f9993d89e5793532d4874.png](../_resources/9f0aa2b9ff1f9993d89e5793532d4874.png)

We are also given the password of the image so lets unlock it by `This PC->Right Click on the drive->Unlock Drive->Enter password`.

After looking into it it contains multiple images:

![da738db525bd6eb2f372d4d6357a0e50.png](../_resources/da738db525bd6eb2f372d4d6357a0e50.png)

Lets analyze the drive in Autopsy to see if we can find some more information:

![95bc3486c0d7f163e6a5641eb8c24f0f.png](../_resources/95bc3486c0d7f163e6a5641eb8c24f0f.png)

All of the images were downloaded from same website except this one image which contains some weird URL encoded data
`HostUrl=https://www.gamewallpapers.com/wallpapers_slechte_compressie/01wallpapers/&#102;&%23108;&%2397;&%23103;&%23123;&%2356;&%2351;&%23102;&%2350;&%2398;&%2348;&%2397;&%2356;&%2399;&%23101;&%2351;&%2357;&%23102;&%2350;&%23101;&%2353;&%2398;&%2397;&%2349;&%23100;&%2354;&%2399;&%2355;&%2348;&%23101;&%2357;&%2355;&%23102;&%2350;&%2357;&%2349;&%23101;&%23125;`

After decoding it we get the flag


# Web
## Socratic-Script

![758ea91fca7953dcff0a35ad06cd43ab.png](../_resources/758ea91fca7953dcff0a35ad06cd43ab.png)

After analyzing the source code we find that the webpage contains a script that prevents us submitting the passphrase

![a3c5572c9d4d6349dff458fff208651c.png](../_resources/a3c5572c9d4d6349dff458fff208651c.png)

We can disable js from dev tools with ctrl+shift+P and select disable js

After we upload the passphrase file that we are given, we get the flag

![5bb6f16afa6d04b86f5994a6f4aab080.png](../_resources/5bb6f16afa6d04b86f5994a6f4aab080.png)

`nicc{p@SSAGe_GR@Nt3D}`

## Into-the-Gorgons'-Den

![089606d0cb148bbd95f718a9fa82e87c.png](../_resources/089606d0cb148bbd95f718a9fa82e87c.png)

This challenge has 3 parts to for the solutions:

### Part 1

After looking at the js code we find that the mirror function just reverses the input and if that input results in "perseus" in reverse we get a hint

![f715fe2f33a48f2aa20e434478794bd3.png](../_resources/f715fe2f33a48f2aa20e434478794bd3.png)

There is also script that sends a request for the solution every minute and it will be revealed only at 28th minute for the server. We wait until we get the solution to the Part 1

![b0dca1e081ca4b5b91156e43b92e933e.png](../_resources/b0dca1e081ca4b5b91156e43b92e933e.png)

At the time of writing I cant get the flag but it was `sl4y`

### Part 2

After analyzing this cipher in dcode.fr we find out that it is ROT-13 Cipher and decode it to get this(You can also try to understand the js to find out that all chars are shifted 13):

![de18a98ce399853ac97f13953e0cf8ad.png](../_resources/de18a98ce399853ac97f13953e0cf8ad.png)

**The second part of the flag is the but the e is a 3 !**

So the solution to the part 2 is `th3`

### Part 3 

We can send all we collected and recieve the final parts solution

![39822dd22743940f9e99bea38b6e90ce.png](../_resources/39822dd22743940f9e99bea38b6e90ce.png)

**nicc{part1_part2_g0rg0n}**

`nicc{sl4y_th3_g0rg0n}`

### Alternative solution(fast):

The `sl4yth3` is hardcoded in the js you can basically visit /fetch_flag.php and get the last part and combine it to get the flag

![6e96af45846dc827ccdb942e3bf2841d.png](../_resources/6e96af45846dc827ccdb942e3bf2841d.png)
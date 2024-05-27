# HackerWebStore
## Description

![51c8abc994640344bc221ba82852cb48.png](../_resources/51c8abc994640344bc221ba82852cb48.png)

## Solution

We have a webpage that allows us to create products and show them:

![7367981ae51c492442310bb139380e22.png](../_resources/7367981ae51c492442310bb139380e22.png)

After some recon we can find out that creating a product is vulnerable to SQLi because putting **single quote** give the following error:

![72e9ec47796cc2f05f03df881ba8f492.png](../_resources/72e9ec47796cc2f05f03df881ba8f492.png)

![429821e03be318be55be8035dbc3d9d2.png](../_resources/429821e03be318be55be8035dbc3d9d2.png)

Now we have our **sink** and its time to weaponize our payload. Its apparent that the error looks like an **sqlite3** error. We can use string concatination `||` to retrieve other information and append it as a value of the given **INSERT** statement.

**Payload:**
First we close the input string with `'` and concatenate the `Select password From users Where id=1` query's result to that empty string. After that we have close the INSERT statement with `);` and comment out the rest with `--`.

So the final payload will look like this:
`'||(Select password From users Where id=1)); --`

![3c30007e904c67a3ba54a4ab4c1e173c.png](../_resources/3c30007e904c67a3ba54a4ab4c1e173c.png)

**Note:**
Although there are proper methods to enumarate the database and table structure we can do some educated guesses for this challange like(users,username,user,pass,password... etc)

Now we can change the payload a bit and get the username of the hash aswell
`'||(Select password From users Where id=1)||(Select name From users Where id=1)); --`

After some recon via changing **id** we get the following users with hashes:

![27d421ee11ed662c1f4f1fb6ee27ae04.png](../_resources/27d421ee11ed662c1f4f1fb6ee27ae04.png)

This is where I got stuck for a long time because the format is not supported by `hashcat` or `john`. After multiple hours of research trial and error i have come across this implementation here(https://defuse.ca/php-pbkdf2.htm) which suggests that the last bit of the hash is hex encoded. The hashcat needs the following format:
`pbkdf2_sha256$iter$salt$hash(b64 encoded)`

So we change the hash of the admin from this `pbkdf2:sha256:600000$MSok34zBufo9d1tc$b2adfafaeed459f903401ec1656f9da36f4b4c08a50427ec7841570513bf8e57`
to this
`pbkdf2_sha256$600000$MSok34zBufo9d1tc$sq36+u7UWfkDQB7BZW+do29LTAilBCfseEFXBRO/jlc=`

Note that for the last part is changed with **hex->binary->base64**

After the conversion we can crack with hashcat using the given wordlist:
`hashcat -m 10000 admin.txt -a 0 wordlist.txt`

Now we can login to the admin account with the password and retrieve the flag!

# The Davinci Code
## Description

![e3468ce44c7d076919e8221b10013886.png](../_resources/e3468ce44c7d076919e8221b10013886.png)

## Solution

![d8c1f33f88ad93d4593d1936f9d26436.png](../_resources/d8c1f33f88ad93d4593d1936f9d26436.png)

We get a simple webpage that we can only navigate to `/code` page which returns an error that contains some debugging information like below:

![74826237e502d438a9e72a9f5c7a48ce.png](../_resources/74826237e502d438a9e72a9f5c7a48ce.png)

Apparently the application tries to open the file `code.html` but it cant find it. After checking the debug information something catched my eye:

![ed3a843c96e485fa137ccc34c7761412.png](../_resources/ed3a843c96e485fa137ccc34c7761412.png)

Lets send a OPTIONS request instead of a GET request with burp suite

![0efb679ce8cb0139886b8d80c2f78ee2.png](../_resources/0efb679ce8cb0139886b8d80c2f78ee2.png)

It also accepts PROPFIND requests which suggest its probably a WebDAV server. After some recon we can also findout that the server accepts the MOVE request aswell which basically moves files across the server. With PROPFIND we can identify the folder structure and find a secret folder called `/the_secret_dav_inci_code` and this folder contains `flag.txt`.

![07e663a69d199e10785a304ac02821af.png](../_resources/07e663a69d199e10785a304ac02821af.png)

![e6825a30222acc7da6013ac91a7766f5.png](../_resources/e6825a30222acc7da6013ac91a7766f5.png)

But when we try to open the page http://challenge.nahamcon.com:31305/the_secret_dav_inci_code/flag.txt we get an 404 not found error.

But why dont we let the server read us instead of trying to read it. MOVE request in WebDAV functions similar to `mv` command in linux which meand that we can rename the file aswell. Since the server tries to open the /template/code.html we can move flag there as a html file. We specify the `Destination` header to the location we want and send the request:

![35d2b0699f81b3e414085cfceb30f575.png](../_resources/35d2b0699f81b3e414085cfceb30f575.png)

Now when we open the /code page we get the flag

![b399985c566ad9581ab030b5c239099c.png](../_resources/b399985c566ad9581ab030b5c239099c.png)




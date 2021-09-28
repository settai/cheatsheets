# Hydra

# **Hydra Commands**

The options we pass into Hydra depends on which service (protocol) we're attacking. For example if we wanted to bruteforce FTP with the username being user and a password list being passlist.txt, we'd use the following command:

`hydra -l user -P passlist.txt ftp://10.10.64.167`

For the purpose of this deployed machine, here are the commands to use Hydra on SSH and a web form (POST method).

## **SSH**

`hydra -l <username> -P <full path to pass> 10.10.64.167 -t 4 ssh`

![https://i.imgur.com/D71vkKM.png](https://i.imgur.com/D71vkKM.png)

[**Post Web Form**](Hydra%20ac0f6ad048004d19bbd8d53ab23eea94/Post%20Web%20Form%20f6e3e59f3af74e72980d131c0885bc3e.md)

We can use Hydra to bruteforce web forms too, you will have to make sure you know which type of request its making - a GET or POST methods are normally used. You can use your browsers network tab (in developer tools) to see the request types, of simply view the source code.

Below is an example Hydra command to brute force a POST login form:

`hydra -l <username> -P <wordlist> 10.10.64.167 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

![Hydra options](options.png)
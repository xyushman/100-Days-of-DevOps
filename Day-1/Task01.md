Create a user named jim with a non-interactive shell on App Server 2

Solution :: 

`thor@jumphost ~$ ssh steve@stapp02.stratos.xfusioncorp.com
steve@stapp02.stratos.xfusioncorp.com's password: 
[steve@stapp02 ~]$ sudo useradd -s /sbin/nologin jim

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for steve: 
[steve@stapp02 ~]$ id kareem
id: ‘kareem’: no such user
[steve@stapp02 ~]$ id jim
uid=1002(jim) gid=1002(jim) groups=1002(jim)
`
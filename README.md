# raspi-exp

<img src=http://core0.staticworld.net/images/idge/imported/article/itw/2014/06/06/tux-linux-professional_0-100520358-orig.png>

## Physical setup

There are two raspberry pi's set up. RPi #1 (pinguas) and RPi #2 (paulo). 

Pinguas is in a firewall-protected network and can only be accessed via ssh. To bypass this, a remote port-forwarding
[reverse-ssh] scheme is setup on port 2210. To set it up, the following steps are taken:

1) Pinguas sshs into paulo with the reverse port-forwarding option set:

`ssh -R 2210:localhost:22 paulo`  

2) Then, paulo can ssh into pinguas by using the command:

`ssh -p 2210 localhost`

3) The keys are added into the appropriate "authorized_keys" file inside the ssh folder, for convenience (no need to keep typing password). We also recommend to setup a [config-file], which removes the need to keep writing the ip address.


## Beginning files

- autossh.service (pinguas)

Runs in background, checking a server. If the server indicates "GO", then pinguas will automatically ssh into paulo as described in setup. In this way, access to pinguas is possible just by turning the physical device on.

## Ideas

- Establish a shared channel. Files copied inside a folder will automatically be copied to the same folder in the other device (dumbed-down dropbox :) ). (Potential solution: https://www.digitalocean.com/community/tutorials/how-to-use-sshfs-to-mount-remote-file-systems-over-ssh )
- Use that channel to send images. 
- Maybe even a stream coming from pinguas' camera? 
-Some idea that involves software development?

[port-forwarding]: http://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html
[reverse-ssh]: https://toic.org/blog/2009/reverse-ssh-port-forwarding/
[config file]: http://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/

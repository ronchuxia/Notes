VNC (Virtual Network Computing) is a remote desktop protocol. 

It works by transmitting screen updates from the server to the client, and sending keyboard/mouse input back. The default port is 5900, with 5901, 5902, etc. for additional displays :1, :2, etc.

Choose a free display number. (Run on the remote machine.)  
```shell
ps aux | grep vnc
```

Run the server. (Run on the remote machine.)  
```shell
vncserver :2 -geometry 1920x1080 -depth 24
```

Tunnel the VNC port. (Run on the local machine.)  
```shell
ssh -L 5902:localhost:5902 <username>@<hostname-or-ip>
```

Connect to `vnc://localhost:5902` through a VNC client. (Run on the local machine.)
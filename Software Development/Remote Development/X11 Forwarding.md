X11 is a display system used by Linux/Unix. It has a client-server architecture:  
- The **X11 server** is the machine with the screen (e.g. your local machine).
- The **X11 client** is the application that wants to draw on a screen (e.g. the remote app).

Normally, apps and display are on the same machine. X11 forwarding separates them: the app runs remotely but sends **drawing commands** to your local display over the SSH tunnel.

Enable X11 forwarding.  
```shell
ssh -X <username>@<hostname-or-ip>
```
NOTE: This requires X11 server installed on the local machine.

`ssh -X` sets the `DISPLAY` environment variable on the remote machine to point back to your local X11 server through the tunnel. Any GUI app you launch then automatically sends its window to your local screen.
Start/stop/kill a service.  
```shell
systemctl start <service>
systemctl stop <service>
systemctl kill <service>
```

Enable/disable (start automatically at boot) a service.  
```shell
systemctl enable <service>
systemctl disable <service>
```

Show status of a service.  
```shell
systemctl status <service>
```
Options:  
- `--user`: Run `systemctl` against the **user-level `systemd` instance** instead of the system-wide one.

Reboot.  
```shell
systemctl reboot
```
Options:  
- `--firmware-setup`: Reboot into UEFI.
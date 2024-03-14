# touchall
This systemd user unit recursively updates file timestamps of files in a given directory (`$SCRATCH`), to overcome the automatic deletion policy generally adopted on HPC clusters. When enabled, the unit will submit a heavily parallelized `touch` command on the whole content of the `$SCRATCH` directory.

## installation
1) Transfer `touchall.service` (and `touchall.timer`) in `~/.config/systemd/user/` (the systemd timer is pointless most of the time, because instances of `systemd-user` seemingly can't survive outside of the login session).

2) Edit the envvars in `touchall.service` accordingly.

3) Run `systemctl --user enable --now touchall.service` to enable and execute the unit immediately.

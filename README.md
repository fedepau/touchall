# touchall
This systemd user unit recursively updates file timestamps in a given directory (`$SCRATCH`) to overcome the automatic deletion policy generally adopted on HPC clusters. When enabled, the unit will submit a heavily parallelized `touch` command on the whole content of the `$SCRATCH` directory at each login.

## installation
1) Transfer `touchall.service` (and `touchall.timer`) in `~/.config/systemd/user/` on the cluster. A systemd timer (which runs the namesake service weekly) is also included, but pointless most of the time, because instances of `systemd-user` seemingly can't survive outside of the login session (at least on the cluster I use).

2) Edit the envvars in `touchall.service` (`TA_PARTITION`, `TA_ACCOUNT` and `TA_SCRATCH`) accordingly.

3) Run `systemctl --user enable --now touchall.service` to enable and execute the unit immediately.

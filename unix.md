# Git Hints and Techniques

## Contents

- [System Monitoring Commands](#system-monitoring-commands)
- [Mapping between runlevels and system targets](#mapping-between-runlevels-and-system-targets)

---

## System Monitoring Commands

```console
$watch -n 5 free -m
```

## Mapping between runlevels and system targets

| Run Level |       Target       |               Description                   |
|-----------|:------------------:|:-------------------------------------------:|
| 0         |  poweroff.target   |  Shut down and power off the system.        |
| 1         |  rescue.target     |  Set up a rescue shell.                     |
| 2, 3, 4   |  multi-user.target |  Set up a non-graphical multi-user system.  |
| 5         |  graphical.target  |  Set up a graphical multi-user system.      |
| 6         |  reboot.target     |  Shut down and reboot the system.           |

To change the current target:

```console
$sudo systemctl isolate multi-user.target
```

To make this the default **runlevel**, you can use followings:

```console
$sudo systemctl enable multi-user.target
$sudo systemctl set-default multi-user.target
```
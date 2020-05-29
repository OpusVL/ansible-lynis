# Ansible Role for Lynis Recommendations

## Principals

After running Lynis against a system a report containing suggestions is output. This report will contain text in the form:

```text
suggestion[]=ACCT-9622|Enable process accounting|-|-|
suggestion[]=ACCT-9626|Enable sysstat to collect accounting (no results)|-|-|
audit_trail_tool[]=auditd
linux_auditd_running=1
suggestion[]=ACCT-9632|Determine the location of auditd configuration file|-|-|
```

I take from this the ID of the suggestion `ACCT-9622` and look it up on the cisofy website:

[https://cisofy.com/lynis/controls/ACCT-9622/](https://cisofy.com/lynis/controls/ACCT-9622/)

After some interpretation I can find the things I need to do to enable the recommendation and then write it into an Ansilbe task within this role.

The suggestions seem to be grouped into ACCT, BANN, KRNL, PKGS id's so I have created tasks for each of these categories. Some recommendations span multiple tasks as you may need to install a package to satisfy an accounting recommendation, eg.

ACCT-9622 - Linux process accounting

This required the installation of the package `acct` and the service needed to be started. So it appears in `PKGS` and `ACCT`.

## Usage

Edit the `production` file and change the `[nodes]` section to include the system(s) you want the tasks carried out on.

Change the value for `syslog_server` in file `group_vars/nodes.yml` to point to the name of your syslog server. The default is just `log`. Logging will be sent to the external log server and recorded locally.

```shell
ansible-playbook site.yml -i production -v
```
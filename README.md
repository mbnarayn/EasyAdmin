# EasyAdmin
**Install Telnet**

`dism /online /Enable-Feature /FeatureName:TelnetClient`

**Suspend BitLocker**

`Suspend-BitLocker -MountPoint "C:" -RebootCount 0`

**Install Chocolatey**

`Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`

**Send Email via Telnet**

`telnet localhost 25`

`ehlo etswap.com`

`mail from: sender@domain.com`

`rcpt to: receiver@domain.com`

`data`

`subject: Test Email via Telnet`

`hello,`

`Email Content`

`Regards`

`Test`

`.`

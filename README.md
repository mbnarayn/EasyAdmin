# EasyAdmin
**Install Telnet**

`dism /online /Enable-Feature /FeatureName:TelnetClient`

**Suspend BitLocker**

`Suspend-BitLocker -MountPoint "C:" -RebootCount 0`

**Install Chocolatey**

`Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`

**Send Email via Telnet**

      telnet localhost 25
      ehlo etswap.com
      mail from: sender@domain.com
      rcpt to: receiver@domain.com
      data
      subject: Test Email via Telnet
      hello,
      Email Content
      Regards
      Test
      .

**Identify Which Domain Controller Authenticated You**

`echo %logonserver%`

**Open the Local Machine Certificate Store**

`certlm.msc`

**Open the Local User Certificate Store**

`certmgr.msc`

**Open Local Users and Computers**

`lusrmgr.msc`

**Open Applications with Elevated Priviliges using Run As Admin Mode**

`Ctrl + Shift + Enter`

**Join Local Computer to a Domain**

`Add-Computer -DomainName domainname.local`

**Join Local Computer to a Domain and Specify the OU on which the computer account should be placed**

`Add-Computer -DomainName example.ac.uk -OUPath "OU=Servers,OU=Azure,OU=Prod,DC=EXAMPLE,DC=AC,DC=UK"`

***
## Disabling AD Replication on a single Domain Controller

**Disable outbound replication from a particular DC**

`repadmin /options DOMAINCONTROLLERNAME +DISABLE_OUTBOUND_REPL`

**Enable outbound replication from a particular DC**

`repadmin /options DOMAINCONTROLLERNAME -DISABLE_OUTBOUND_REPL`

**Disable inbound replication from a particular DC**

`repadmin /options DOMAINCONTROLLERNAME +DISABLE_INBOUND_REPL`

**Enable inbound replication from a particular DC**

`repadmin /options DOMAINCONTROLLERNAME +DISABLE_INBOUND_REPL`

**How to check if replication is enabled or disabled?**

> When replication is disabled, warning events 1115 (for disabled outbound replication) or 1113 (for disabled inbound replication) from source NTDS General will be logged in the Directory Service event log during system startup. As far as I am aware, no events are regularly logged during normal operation to indicate that replication is disabled. When replication is re-enabled, informational events 1116 (for outbound replication) and 1114 (for inbound replication) are logged.

***


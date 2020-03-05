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



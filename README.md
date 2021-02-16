# EasyAdmin
**Install Telnet**

`dism /online /Enable-Feature /FeatureName:TelnetClient`

**Open Hosts File with Elevated Admin Privileges**

`powershell.exe -Command "Start-Process 'Notepad.exe' -Argument 'C:\Windows\System32\drivers\etc\hosts' -Verb RunAs"`

**Add Hosts Files Entry with a Batch File**

Create a batch file with .bat extension similar to the below (replacing the domain names and IPs). Then run the batch file with elevated admin rights. This will append (will not replace or delete any existing entries but only adds) the entries to the hosts file.

      @echo off
      set hostspath=%windir%\System32\drivers\etc\hosts
      echo 127.0.0.1 www.domainname.com >> %hostspath%
      echo 127.0.0.1 www.domainname.co.uk >> %hostspath%
      exit

**Change Network Connection Profile to Private**

`Get-NetConnectionProfile | Set-NetConnectionProfile -NetworkCategory Private`

**Suspend BitLocker**

`Suspend-BitLocker -MountPoint "C:" -RebootCount 0`

**Force Azure AD Sync**

`Start-ADSyncSyncCycle -PolicyType Initial`

**Copy Group Memberships from One Group to Another**

      $gsource = "Source Group Name"
      $gtarget = "Target Group Name"
      Get-ADGroupMember -Identity $gsource |
      foreach {
      Add-ADGroupMember -Identity $gtarget -Members $($_.DistinguishedName)
      }

**PowerShell Comparison Operators**

Return all results with an occurence of vi anywhere in the username, for example David.

`Get-CsOnlineUser -Filter {UserPrincipalName -like '*vi*'} | select UserPrincipalName`

Only return results have an exact match.

`Get-CsOnlineUser -Filter {UserPrincipalName -eq '*JoeBloggs@domain.co.uk*'} | select UserPrincipalName`

Return all result starting with vi, for example Victoria.

`Get-CsOnlineUser -Filter {UserPrincipalName -like 'vi*'} | select UserPrincipalName`

**PowerShell Get a Count of the Results**

`Get-CsOnlineUser -Filter {UserPrincipalName -like 'vi*'} | select UserPrincipalName | measure`

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

**Use Robocopy to Copy All Files, Folders and Permissions from Source to Destination**

`robocopy "C:\sourcefolder" "C:\destinationfolder" /MIR > "copylog.txt"`

Use this command very carefully. The /MIR switch will delete any existing files or folders in the destination directory if it does not exist at source. It will never delete from source. The command is a one way mirror from source to destination.

**Exporting Contents of a Primary Mailbox or Archive to a PST File**

`New-MailboxExportRequest -Mailbox JoeBloggs -FilePath "\\SERVER01\PSTFileShare\JoeBloggs_PrimaryMailbox.pst"`

This example exports the user's primary mailbox to a .pst file on the network shared folder PSTFileShare on SERVER01.

`New-MailboxExportRequest -Mailbox JoeBloggs -FilePath "\\SERVER01\PSTFileShare\JoeBloggs_Archive.pst" -IsArchive`

This example exports the user's archive to a .pst file on the network shared folder PSTFileShare on SERVER01.

Both the above cmdlets requires the admin to be assigned the Mailbox Import Export role, and by default, the role isn't assigned to any role groups. Also note that the -FilePath value only accepts UNC paths.


***
## Setting Up Exchange Email Forwarding to External Email Address Without Creating a Mail Contact

By default to forward mail externally for an Exchange Mailbox User you must create a Contact. If you configure email forwarding to an external email address without creating a mail contact the forwarding will not work.

To set up forwarding to an external email address without creating a contact, the Exchange Administrator will need to add a remote domain using the command below. Remote domains are SMTP domains that are external to your Microsoft Exchange organization.

```
New-RemoteDomain -Name ExternalDomain -DomainName externaldomain.com
```

Once you have added the remote domain, run the below command to check that Auto Forward is enabled.
```
Get-RemoteDomain ExternalDomain | Select DomainName, AutoForwardEnabled 
```
Now to forward email for a user to an external email address as well as deliver a copy to their primary mailbox run the command below:

```
Set-Mailbox -Identity joe.bloggs@domain.com -DeliverToMailboxAndForward $true -ForwardingSMTPAddress Joe.Bloggs@externaldomain.com
```
The above command also works for Shared Mailboxes.
Email forwarding to external addresses cannot be configured via the GUI. Also it not possible to view the forwarding from the GUI when using this method.

To view the forwarding SMTP address use the cmdlete below:

```
Get-Mailbox -Identity joe.bloggs@domain.com | Select Name, ForwardingSMTPAddress
```

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


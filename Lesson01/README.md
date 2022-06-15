#01 Installing the Domain Controller

0. Use `sconfig` to:
    - Change the hostname (DC1)
    - Change the IP address to static
    - Change the DNS server to own IP address

1. Enable Remote management from Mnagement client(Windows 11 machine)
    - On the Server:
        * Enable-PSRemoting
        
    - On the management client:
        * start Windows Remote Managemt service (`Start-Service WinRM`)
        * Add server to the Trusted Hosts list for WinRM client (`Set-Item wsman:\localhost\Client\TrustedHosts -value <server-ip-address>`)
        * start new PowerShell session on the remote server and provide login credentials to the server (`New-PSSEssion -COmputerName <server-ip-address> -Credential (Get-Credential)`)
        * remotely login into the server with cmdlet pipeline position Id, usually "1" (`Enable-PSSession <id>`)


2. Install the active Directory Windows Feature (`Install-WindowsFeature AD-Domain-Services -IncludeManagementTools`)

3. Import ADDS deployment module (`import-Module ADDSDeployment`)
4. Install ADDSForest (server dns server changes to a loopback address and WE NEED TO CHANGE THIS)
5. Find out the nerwork Interfaces and index with the loopback address (`Get-DNSClientServer Address`)
5. set the server address to the prefered ip (`Set-DNSClientServerAddress -InterfaceIndex <index value> -ServerAddress <ip address>`)


resources: 
1. https://xpertstec.com/how-to-install-active-directory-windows-server-core-2022/
2. https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services--level-100-
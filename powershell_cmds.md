Check if ports are enabled. USeful when telnet or cmd is disabled 

<b>New-Object System.Net.Sockets.TcpClient("192.168.0.2", 80) <b>

*****************************************************************************************

function Get-ByOwner
 {
   Get-ChildItem -recurse C:\ | get-acl | where {$_.Owner -match $args[0]} 
 }

PS C:\> Get-ByOwner JackFrost

*****************************************************************************************

WMI objects

# Computer System
$ComputerSystem = Get-WmiObject -Class Win32_ComputerSystem -ComputerName $ComputerName
# Operating System
$OperatingSystem = Get-WmiObject -Class win32_OperatingSystem -ComputerName $ComputerName
# BIOS
$Bios = Get-WmiObject -class win32_BIOS -ComputerName $ComputerName


Powershell split command 

$filename = "sample.cfg"

Get-Content $filename | ForEach-Object {
    $_.split(":")[1]
}


Getting a list of excel files and printing only the name of the file. 

 Get-ChildItem -File -Name -Recurse |  ForEach-Object {$_.split("\")[1]} >                                                

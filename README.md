# hello-world
Powershell script changing multiple different default gateways
#### Below is a summary of what I have done and am trying to do

Looking for direction here. 

Fairly novice still to PS.  I have written a script that does the following

1.) logs in to my vcenter,selects a particular datacenter, grabs all the vm's in that datacenter in to a variable
2.) ForEachs that list VM by VM to get me the following info I need....computername, IP and DefGW (see command below i am using)

	gwmi -Class Win32_NetworkAdapterConfiguration -ComputerName $RemoteComputer | Where { $_.IPEnabled -eq $OnlyConnectedNetworkAdapters -and ($_.DefaultIPGateway -like "*.10")  } | 

Select-Object $Output
	
3.) Formats and kicks that out to a CSV so I end up with a CSV that looks like this (raw in notepad)..pasting the first few lines so you get an idea

	"PSComputerName","IPAddress","DefaultIPGateway"
	"websrv02","192.168.3.42","192.168.3.10"
	"appsvr03","192.168.24.212","192.168.24.10"
	"server02","192.168.24.209","192.168.24.10"

4.) I have a huge list of servers that I need to move to our other datacenter...as you can see, each server's DG ends with *.10, but the server list is on all diff subnets

5.) Anything with a .10 gateway, needs to be changed to a .246 gateway....on the same subnet it is currently on.  so just gonna change the last octet to .246

so I am trying to script changing the DG on each server to the proper .246 in its subnet.  I need to find a way to have powershell change it by saying "if DG = 192.168.3.10 then (via 

powershell command) change IP of DG to 192.168.3.246...but if the DG = 102.168.24.10 then (via powershell command) change IP of DG to 192.168.24.246", etc,etc


Not fully knowing how to do this, I added to the script this info I can call on as variables...again...dont know how I will use them...but I defined them as follows

########
# Variables below define the DG's of current(source) and new(destination) 

$3 = "192.168.3.10"
$24 = "192.168.24.10"
$44 = "192.168.44.10"
$225 = "10.42.225.10"
$199 = "192.168.199.10"

$R3 = "192.168.3.246"
$R24 = "192.168.24.246"
$R44 = "192.168.44.246"
$R225 = "10.42.225.246"
$R199 = "192.168.199.246"

Any help anyone can provide would be greatly appreciated. DO I load the CSV in to an array?  How would I do the IF statememt to change it to the correct DG for each server?  

	

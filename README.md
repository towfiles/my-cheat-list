# Developer Cheat-list
These are compilations of commands and tools i use in solving the issues:

 - **TCP dump**:
	 - TCP dump is a powerful tool which is used for listening to request and response coming into a Unix based system. it is installed by default therefore you do not need to worry about installation. you could use TCP dump to troubleshoot the following types of issues:
			 - HTTP response data is not what you are expecting
			 - checking HTTP request data send and the response sent to know what your app server is receiving and how its responding
			 - to open tcpdump mode run the following: `tcpdump -s 0 -A 'tcp dst port 80 or tcp dst port 443 and tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420 or tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x504F5354 or tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x48545450 or tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x6a736f6e'`
			 - this TCP command captures HTTP, POST and GET JSON request (never tested it with XML yet)
 -  **Check a servers public IP**	 
	 - there might be scenarios where we are being asked to provide our public ip so another game provider or system can whitelist them
	 - to check this you can either check the device list from rackspace OR run the following command: `dig +short myip.opendns.com @resolver1.opendns.com`
 - **Reading logs**
	 - ability to read and trace server logs is a very powerful functionality that you could easily use to find the root cause of problems. the Linux tail command is the best tool you need for these kinds of challenges. a typical example is: `tail -f -n 1000 /var/www/cageapi/log/cageapi.log`
	 - you could combine tail with the powerful command like grep (grep filters out any text written on the console). a typical example is:  `tail -f -n 1000 /var/www/cageapi/log/cageapi.log | grep -A 10 -B 10  amatic`
	 - the above log basically read last 1000 lines of cageapi log and searches for occurence of “amatic” in a way that the 10 lines above and below are displayed.
 - **Understand shell commands**
	 - I discovered this awesome website: [explainshell](https://explainshell.com/ "https://explainshell.com/") in which all you need to do is to paste a shell command in the text field and it will explain what the command does along with what each argument/parameters does
 - **Understanding and writing Regex**
	 - Another Powerful tool I use is [https://regexr.com/](https://regexr.com/ "https://regexr.com/") with this website you can paste in a regular expression and text in which it will basically show you all the characters/strings that matches the expression
 - **Troubleshooting connectivity issues**
	 - I mostly use the telnet utility tool to check for remote connectivity of servers either with hostname or ip with their port numbers. Telnet utility allows users to test connectivity to remote machines and issue commands through the use of a keyboard. Though most users opt to work with graphical interfaces, Telnet is one of the simplest ways to check connectivity on certain ports.
	 - the beauty of telnet is that is could run on almost every single OS that i know of (although some of them do not have telnet installed b default)
	 - basically you can use telnet to test maybe a port is open or not or even if the server is reachable all you need is just run the following: `telnet rpc.acronis.com 443` for example, the command checks if port 443 is open and rpc.acronis.com is connectible as well. another example is like trying to test if you can connect to a mysql server: `telnet mydb 3306` where mydb is mysql host or IP and 3306 is the standard mysql port

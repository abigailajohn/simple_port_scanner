# simple_port_scanner
import sys
import socket
from datetime import datetime
import pyfiglet


ascii_banner = pyfiglet.figlet_format('SIMPLE PORT SCANNER')
print(ascii_banner)

#define our target
if len(sys.argv) == 2:
    #translate hostname to IPv4
    target = socket.gethostbyname(sys.argv[1]) 

else:
    print("invalid amount of arguments.")
    print("Syntax: python3 socket.py <ip>")

#adding a banner
print("#"*50)
print("Scanning Target"+ target)
print("Scanning started at:" + str(datetime.now()))
print("#"*50)


try:
    #you can choose the range of port you want to scan.
    for port in range(1,1000):
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        socket.setdefaulttimeout(1)

        #returns an error indicator 
        result = s.connect_ex((target,port))
        if result == 0:
            print("Port {} is open".format(port))
        s.close()

except KeyboardInterrupt:
    print("\n Exiting Program !!!")
    sys.exit()

except socket.gaierror:
    print("\n Hostname could not be resolved !!!")
    sys.exit()

except socket.error:
    print("\n Server nor responding !!!")
    sys.exit()

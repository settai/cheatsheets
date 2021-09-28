# Netcut

- Start web server :

 python3 -m http.server 80

- Create a netcat listener (reading from and writing to network connections using TCP or UDP)

 nc -nvlp port  

-n : Do not do any DNS or service lookups on any specified addresses, hostnames or ports.

-v : Have nc give more verbose output.

-l : Used to specify that nc should listen for an incoming connection rather than initiate a connection to a remote host.

-s  *source_ip_address :*  Specifies the IP of the interface which is used to send the packets.

-p source_port : Specifies the source port nc should use.

-e specify which program to execute after connecting to a host

-u connect to udp ports

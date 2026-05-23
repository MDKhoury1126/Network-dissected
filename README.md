# Network-dissected
```import socket

mysock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
#socket.socket(address family, socket type)
#socket.AF_INET = Address Family: Inernet(IPv4)Communicate using IPv4 addresses
#Sock_Stream = TCP socket (reliable, connection-oriented, stream based protocol.
Sock_stream – TCP
Sock_DGRAM – UDP
HTTP runs on TCP not UDP         (HTTP – HyperText Transfer Protocol)
Port 80 is a default TCP port

mysock.connect(('data.pr4e.org', 80))
# mysock.connect(host name, port)(tuple) establishes TCP connection from my machine to the remote host and port.
''''URL that was given in problem = http://data.pre4.org/intro-short.txt
URL (Uniform Resource Locator): scheme://host:port/path
	Scheme http
	Host data.pre4e.org
	Port not written but defaults to 80 for HTTP
	Path /intro-short.txt''''

cmd = 'GET /intro-short.txt HTTP/1.0\r\nHost: data.pr4e.org\r\n\r\n'.encode()
# cmd is a variable (not command prompt)
''''Get HTTP method asking server to retrieve a resource
/intro-short.text the path part of the URL
HTTP/1.0 HTTP version you are speaking
\r\n Carriage return and line feed end of header line 
Host: data.pre4e.org This is an HTTP header. Tells server which hostname you are trying to reach. 
\r\n\r\n marks end of all headers (blank line)
‘’ because everything inside the ‘’ is a Python string literal. If no quotes Python would think GET is a variable and the rest as invalid syntax. .encode is not in quotes because it is not part of the string message you are sending but rather an action, a Python method (a function that belongs to an object.
.encode converts string into bytes object using a default encoding (UTF-8)''''

mysock.send(cmd)
# sends variable cmd which is the request encoded in bytes

while True:
    data = mysock.recv(512)
    if len(data) < 1:
        break
    print(data.decode(), end='')
# while True: starts an infinite loop
''''data (variable)mysock.recv(512) returns bytes at 512 bytes at a time.
if len(data) < 1: break if length of data returned is less than one then no more data and server closed connection
data.decode()converts bytes into a string
end=’’ prevents print() from adding its own newline; the data already contains its own \r\n sequences so you don’t need extra blank lines.''''

mysock.close()
# closes TCP connection


---
layout: post
title: "Simple Ruby DB"
date: 2017-10-05T12:12:00-04:00
tags: programming
---

I wanted to implement a super simple database using TCP. I have been using a lot of Rails lately and I'm trying to remember the basics of the protocol (and Ruby!). I really love Practicing Ruby so I decided to revisit a post I read there a while back. The following is pretty much directly taken from [Practicing Ruby](https://practicingruby.com/articles/implementing-an-http-file-server), but in my own words.

I want to implement a simple webserver in ruby to setup my database on a specific port. First, we need HTTP, how this works:

* The browser issues a request by opening a TCP (transport control protocol) socket connection to a specific address' port. The server accepts and opens the socket for bi-direcitonal communication.
* When the connection is made, the HTTP client sends a HTTP request.
* The server parses the request for method, URI, etc. 
* Using the same connection, the server responds with the contents or body of the request
* Once done, the server closes the socket to terminate the connection.

So to write this we will:

* Require socknet, a bunch of ruby TCPServer and TCPSocknet classes.
* Initialize a TCPServer object that will listen on a port for incoming connections
* Keep this in a loop processing one incoming connection at a time
* Wait until a client connects, then return a TCPSocket that can be used in like anyother input/output object.
* Read the first like of the request `socknet.gets`
* Log the request to the console where we are running the program (can be removed, just debugging)
* Print the request with content-type, length, etc.
* Print the response body (so it shows up on our webpage)
* Close the socket

```
require 'socket'
server = TCPServer.new('localhost', 4000)

loop do
  socket = server.accept
  request = socket.gets
  STDERR.puts request
  response = "Hello World!\n"
  socket.print "HTTP/1.1 200 OK\r\n" +
                "Content-Type: text/plain\r\n" +
                "Content-Length: #{response.bytesize}\r\n" +
                "Connection: close\r\n"
  socket.print "\r\n"
  socket.print response
  socket.close
end
```

This seems like a lot! Since I know I have to include more code, I'm going to take a look at `rack`, which is a minimal interface between servers that supports ruby. What's nice about this simple server though is that I know exactly what it's doing and I can limit it to one port. `rack` gives us a ton of stuff under the hood.

So continuing with our simple little web server and port, we can write a simple db in memory for storing keys:

```
require 'socket'
require 'uri'

DB = Hash.new

def run(server)
  loop do
    socket = server.accept
    request = socket.gets
    db = fetch(request)
    STDERR.puts request
    response = "#{db}!\n"
    socket.print "HTTP/1.1 200 OK\r\n" +
                  "Content-Type: text/plain\r\n" +
                  "Content-Length: #{response.bytesize}\r\n" +
                  "Connection: close\r\n"
    socket.print "\r\n"
    socket.print response
    socket.close
  end
end

def fetch(request)
  uri = URI.parse(url)
  db_method = uri.path
  if db_method == '/get'
    key = uri.query.split('=').last
    message = "key stored at #{key} is #{DB[key]}"
  elsif db_method == '/set'
    key = uri.query.split('=').first
    value = uri.query.split('=').last
    DB[key] = value
    message = "setting #{key} to #{value}"
  else
    message = 'error'
  end
  return message
end

server = TCPServer.new('localhost', 4000)
run(server)
```

Now we can set the value for any key like:

```
localhost:4000/set?somekey=somevalue
```

And access these keys like so:

```
localhost:4000/get?key=somekey
```

We've now implemented a simple key/value store in-memory! This is pretty cool and only took me about half an hour to throw together. Getting back to basics is fun. Next, I want to expand on this by developing a file system to store this database outside of memory.
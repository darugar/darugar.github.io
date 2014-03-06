---
layout: parand
title:  "Simple Recipe for Debugging Web Services"
date:   2005-03-11 10:00:00
categories: stddev
---
Debugging Web services seems to be a black art, entirely related to your knowledge of the arcane details of your SOAP toolkit. Here's one approach I've found useful:

A SOAP call is just XML over HTTP. All you have to do is capture the XML sent by the SOAP client, inspect it, modify it as you like, and send it to the SOAP provider. 

Grab yourself a copy of [netcat](/web/20101222021439/http://netcat.sourceforge.net/). This is a great little command line utility that "reads and writes data across network connections, using the TCP/IP protocol." You can use it to capture data and send data on a socket very simply, which is what HTTP is about. Unfortunately I don't think there's a windows version; there are alternatives, but I'm too lazy to dig.

Compiling and installing this thing is a breeze, and trust me, you'll be happy you did. It's quite a useful little tool. You can follow the supplied instructions for installation, or just do this:

`tar zxvf netcat-0.7.1.tar.gz  
cd netcat-0.7.1  
./configure  
make  
cp src/netcat /somewhere/in/your/path  
`

Once you have netcat running, setup it up as a listener:  
`netcat -l -p 9000`

Now point your web browser at it:  
http://youraddress:9000/test/path

You should see the HTTP request on the command line where you're running netcat, and your browser waiting for a reply. Since you haven't told netcat to return any data, it'll just sit there. Hit stop on your browser. Congratulations, you've just captured data over a socket.

To make this useful, you'll probably want to put the captured the data into a file:  
`netcat -l -p 9000 > incomingrequest.data`

Ok. Now let's try it with SOAP. Setup netcat to listen on port 9000 as shown on the line above. Now, point your SOAP client at it. Take your existing client, and set the 'endpoint' or 'proxy' or whatever your toolkit wants to call it, to `http://youraddress:9000/test` .

Run the client. It'll send the request, the request will get captured by netcat, and it'll sit there since there is no reply from netcat. Hit Ctrl-C on the netcat command line.

Now you can take a look at the incomingrequest.data file to see what your SOAP client is actually sending out. This may be the end of your debugging; you may see something you need to fix.

If not, we need to take the next step and send the request to the actual SOAP service. This is pretty easy:

`cp incomingrequest.data outgoingrequest.data`

Open outgoingrequest.data in an editor. You'll see something like this:

`  
POST /test HTTP/1.0  
Content-Type: text/xml; charset=utf-8  
Accept: application/soap+xml, application/dime, multipart/related, text/\*  
User-Agent: Axis/1.2RC2  
Host: youaddress:9000  
Cache-Control: no-cache  
Pragma: no-cache  
SOAPAction: ""  
Content-Length: 411  
`

Followed by the XML for the SOAP message. This is the request sent by your SOAP client in all its glory. The very first line and the very last line are the ones you care about. Modify the first line, changing `/test` to whatever path the soap provider lives at. How do you find the value for this? By looking at the WSDL for the service. As an example, open up the XMethods stock quote WSDL:  
[http://services.xmethods.net/soap/urn:xmethods-delayed-quotes.wsdl](/web/20101222021439/http://services.xmethods.net/soap/urn:xmethods-delayed-quotes.wsdl)

You're looking for the location attribute of the address element under the port element, which typically appears at the very end of the WSDL file. In this case:  
`<soap:address location="http://64.124.140.30:9090/soap"/>`

So the location is `http://64.124.140.30:9090/soap` , and the path we're looking for is the piece after the third slash, `/soap`. 

Change /test to /soap in your outgoingrequest.data file. Now you're ready to send the request to the provider. Run netcat as:

`netcat 64.124.140.30 9090 < outgoingrequest.data`

This sends the request that you captured to the service provider, and captures the response from the provider. You may want to capture it to a file:  
`netcat 64.124.140.30 9090 < outgoingrequest.data > incomingresponse.data`

There you have it. Now you've seen both the request and the response. If you want, you can modify the request and see how the server responds. This is very easy; just modify the XML in the outgoingrequest.data file as you like. The only thing you have to pay attention to is the Content-Length of the request, the last line of the headers we saw above. Make sure you update this to be accurate. If you add five extra characters to your SOAP message, increase the Content-Length header by five. You get the idea.

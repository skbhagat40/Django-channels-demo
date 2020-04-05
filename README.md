# Django-channels-demo
A simple chat room using Django channels.

Django channels -
Uses ASGI, like but handles async requests like websockets.
WSGI was built for synchronous http protocols. It takes a request and returns a
response.
However, It cannot work with protocols like websockets where a connection is long lived and 
request/response can be sent anytime.
So, ASGI takes the core of django and wraps it with asynchronous layer. It is backwards compatible with WSGI.
Popular WSGI server - gunicorn. Popular ASGI server - daphene.

Server Gateway Interface - It acts like a bridge between Web Servers like nginx and python application. It is responsible
for calling your application, mantaining threads etc.

Basic Functioning of ASGI - 
Scopes and Context -

ASGI takes your request and creates a scope entry (which is a dict) which stores information about the connection.
The scope lasts till the connection lasts. For HTTP connections it lasts till single response cycle.

A part of ASGI application is Consumers which consume requests. ASGI provides Consumers with three main attributes  context, send and recieve attributes.
send allows them to send message via websocket connection. recieve allows them to recieve messages and context contains information about the request itself.

A major difference between ASGI  and WSGI is that is WSGI an application is a callable, while in ASGI for a request an application <b>instance</b> is created and it is <b> run inside the event loop. </b>

The Concept of Channel Layers - 
Channel layers allow several application instances to communicate with each other.

A channel layer has following concpets - 

 1. Channel Layer - There is a unique channel layer for each application instance.
 2. Groups - Collection of Channel layers. Those with group name can add channel layers to the group and send messages to 
 all channel layers in the group. (Group Send).
 
 A common usecase would be chat room where a room is a group of channel layers where each channel layer represents a user.

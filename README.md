<p align="right"><img src="https://github.com/isc-at/CPIPE/blob/master/archived.jpg"/></p>

#### Version 2 added
Updated according OEX templates    
Removed hand crafted containers in favor of standard distibutions   
New instructions added   
### Inspiration
Using the IRIS native API for Node.JS was the oportunity to present a MicroService operating in a Docker container.  
__A demo video is now also available to [watch the demo](https://youtu.be/dSV-0RJ5Olg) in operation.__   
### What it does
This WebSocketClient Service runs in an own container checking for messages to be submitted using IRIS native API for Node.JS.  
The service operates with 3 Globals (Run/Stop WSserver, Input, Output)  
Data are fetched from IRIS and sent to an external WebSocket Echo Service and reply is written back to IRIS.  
All information is provided from IRIS.  
To visiualize operation the containr should run interactive.  
Control / Input / Output is all managed from a interactive utility in IRIS.     
### Challenges I ran into
- run a vanilla IRIS distribution out of the box __without docker-compose__
- transform interface from Caché into new IRIS native API. 
### Accomplishments that I'm proud of
- No need for ZPM or docker-compose.  
- A single docker container does it all.  
- Run the same image on native Docker (Linux) and Docker Desktop for Windows,
  (had no acces to MAC)  
- Build an [All-in-1 image](https://openexchange.intersystems.com/package/IRIS-NativeAPI-Nodejs-compact) with Sevice and IRIS in a common container.    
### What I learned
- Handling and running more than 1 Docker container in cooperation.  
- Working with Docker volumes.  
- Limits of Docker Desktop for Windows    
### Built with
- IRIS Community Edition in Docker  
- IRIS native API  
- Node.JS  
- Docker utility functions
### Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.   
#### Version 1
Pull and init the demo:  
- __docker pull store/intersystems/iris-community:2020.2.0.204.0__  
- __docker pull rcemper/rcc:demoJS__   
- __docker run --name ini1 --init -it --rm --privileged -v vol1:/external rcemper/rcc:demoJS bash /rcc/init.sh__   
[Detailed description](https://github.com/rcemper/WSockClientMicroSV/blob/master/READMEwindows.MD)    
##### How to Work With Version 1
Run first a Docker exec session for the Control / In-Out utility in IRIS     
__docker run --name iris1 --init --rm -d -p 52773:52773 -p 51773:51773 -v vol1:/external store/intersystems/iris-community:2020.2.0.204.0 -b /external/pre.copy__  
Next start the Service process   
__docker run --name rcc1 --init -it --rm rcemper/rcc:demoJS /usr/bin/node /rcc/nodejs/WSockIris.js 172.17.0.2__ 
And start the control program for IRIS in a new command / terminal session   
__docker exec -it iris1 iris session iris ZSocket__    
### Version 2     
download the repo to local directory and run      
- __docker-compose up -d__    
#### How to Work With Version 2      
Start the IRIS session    
- __docker-compose exec iris iris session iris ZSocket__  
       
Open a new terminal window and start the Service container      
- __docker-compose exec nodejs node WSockIris.js__    

Detailed descriptions:    
[Read more](https://github.com/rcemper/WSockClientMicroSV/blob/master/READMORE.md)    
[Readme Windows](https://github.com/rcemper/WSockClientMicroSV/blob/master/READMEwindows.MD)  
[Article in DC](https://community.intersystems.com/post/websocket-client-js-iris-native-api-docker-micro-server)    

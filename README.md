# DHCP Server
This project use ISC-DHCP configuration to run an dhcp
server with an UI for server management

## Dependencies

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Configuration
The server use an DHCP configuration into [dhcp.conf](./isc-dhcp/dhcp/dhcpd.conf) file.

Edit this file to config your own server.

## Installation
After cloned this repo, ensure you are on the root of the project.

Use docker-compose to deploy the server:
```
docker-compose up
```
After that the server is ready to receive dhcp request on port 67.

Access the UI management from http://localhost:3000

## Documentation 
 - IMAGE: The image used is [djaydev/glass-isc-dhcp](https://hub.docker.com/r/djaydev/glass-isc-dhcp) from dockerhub
 - ENVIRONMENT:
    - ADMINPASSWORD: ui admin password (username still the same)
    - WEBADMINPORT: ui server port (default 3000)

The compose file:
``` yml
version: "3"
  
services:
  dhcp: # the dhcp service
    image: djaydev/glass-isc-dhcp # the dhcp docker image from dockerhub
    network_mode: host # use the host network mode for the container 
    volumes:
      - ./isc-dhcp/dhcp:/etc/dhcp:rw  # map the dhcpd.conf file with the container
      - ./isc-dhcp/leases:/var/lib/dhcp:rw
    environment: 
      TZ: Atlantic/Cape_Verde # server timezone
      ADMINPASSWORD: glassadmin # ui admin password as well username
      WEBSOCKETPORT: 8080 # ui socker port
      WEBADMINPORT: 3000 # ui server port
```


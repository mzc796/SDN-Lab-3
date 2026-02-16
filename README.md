# SDN-Lab-3
Configure flow entries via OpenDaylight northbound interface

Continue with SDN-Lab-2, now let's configure flow entries via the OpenDaylight northbound interface 
## Virtual Machine Summary
Memory: >= 8GB

Storage: 50GB

CPU: 2 cores, AMD64 Architecture

Installation Disc: [ubuntu-22.04.4-desktop-amd64.iso](https://old-releases.ubuntu.com/releases/22.04/)

## References
[An Instant Virtual Network on your Laptop (or other PC)](https://mininet.org/)

[PICOS 4.4.3 Configuration G](https://pica8-fs.atlassian.net/wiki/spaces/PicOS443sp/overview?homepageId=10453009)

[OpenDaylight Flow Examples](https://docs.opendaylight.org/projects/openflowplugin/en/latest/users/flow-examples.html)
## Start SDN testbed
1. Open a terminal, start OpenDaylight:
   ```
   cd karaf-0.20.1/bin
   sudo ./karaf
   ```
2. Open another terminal, start Mininet. :
   ```
   sudo mn --custom ~/lab-1/topo-2sw-2host.py --topo mytopo --switch ovsk,protocols=OpenFlow13 --controller remote,ip=127.0.0.1,port=6653
   ```
3. Open the 3rd terminal to request nodes to verify the connection:
   ``` 
5. In the mininet terminal:
   ```
   h1 ping h2
   ```
   Question: Was the `ping` successful? Why?
4. 

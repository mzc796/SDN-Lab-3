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
   sudo mn --custom ~/custom_mn/topo-2sw-2host.py --topo mytopo --switch ovsk,protocols=OpenFlow13 --controller remote,ip=127.0.0.1,port=6653
   ```
3. Open the 3rd terminal to request nodes to verify the connection:
   ```
   mkdir data
   cd odl/
   sudo ./read_nodes.sh
   ```
   Read the file `data/nodes.json`. If it has statistics, the connection is successful.
   
4. Try `ping`. In the mininet terminal:
   ```
   h1 ping h2
   ```
   Question: Was the `ping` successful? Why?
   
5. Use OpenDaylight Rest API to configure ARP flow entries

   (1) Refer to `odl/arp_odl.sh` to configure the ARP flow entries for each switch.
   
   NOTE: The format of dest IP address is `10.0.0.1/32`. Search what does `10.0.0.1/32` mean?

   (2) Request the config data store on the OpenDaylight. On a terminal:
   ```
   cd odl/
   sudo ./read_config_flows.sh $SW_ID
   vim data/$SW_ID_config_flows.json
   ```
   If the json file has content as expected, the flow entry is configured successfully.

   (3) Check the flow entry on the mininet. On a terminal:
   ```
   cd mn/
   sudo ./dump-flows.sh $SW_ID
   ```

   If the flow entry is indeed on the mininet switch, this configuration is successful.

   (4) Finish the flow entries on both switches to enable complete ARP packet exchanges.

   (5) On the mininet terminal, check arp table on both host, e.g.,
   ```
   h1 arp
   ```
   Continue until `h1 arp` and `h2 arp` have complete arp tables.
   
6. Use OpenDaylight Rest API to configure ICMP flow entries
   
   (1) Refer to `odl/icmp_odl.sh` to configure ICMP flow entries for each switch.

   (2) Finish the flow entries on both switches to enable complete ICMP packet exchanges, until `h1 ping h2` is successful.

7. Understand the config and nonconfig data store
   
   (1) Shut down OpenDaylight with `control + D`. Restart mininet and read flow entries on the mininet end. Keep in mind your observation.

   (2) Restart OpenDaylight. Read flow entries on the mininet end.
   
   Question: What do you observe? Why?

8. Practice flow entry setup with [examples](https://docs.opendaylight.org/projects/openflowplugin/en/latest/users/flow-examples.html)
   (1) Install xterm:
   ```
   sudo apt install xterm
   ```
   (2) Open hosts' terminals. In the mininet terminal:
   ```
   h1 xterm
   ```
   You should see a black terminal coming out. That's the `h1`. Do the same thing for `h2`.
   (3) Send IP packets from Host 1 to Host 2 with Scapy

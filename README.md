# Geotemporal
Geotemporal-cast: spatio-temporal dissemination protocol for VANETs.

Geotemporal was coded and tested with NS-3 version 3.25.

## Usage

Copy the ``geotemporal`` folder to the ``/ns-allinone-X.YY/ns-X.YY/scratch`` folder (X.YY is the version of the NS-3 you are using).

To run you must use the following command:
```
./waf --run "scratch/geotemporal/geotemporal"
```

You can specify some parameters using the following sintax (see ``GeotemporalInstaller::Configure (int argc, char **argv)`` method from ``geotemporal/geotemporal-installer.cc``):
```
./waf --run "scratch/geotemporal/geotemporal --sourceNodesList=0,1,2,3,4 --packetsPerSource=4 --packetsLength=1024 --dataRate=1000 --vehiclesDensity=60 --seed=1 --nodesToStartInArea=2 --deltaDistance=20 --replicasPerPacket=3 --checkDataProgress=false --xmlOutput=true"
```

Geotemporal writes XML events to the output stream, to store the output in a file use the following sintax:
```
./waf --run "scratch/geotemporal/geotemporal" > output-files/geotemporal/geotemporal_output.xml 2>&1

or 

./waf --run "scratch/geotemporal/geotemporal --sourceNodesList=0,1,2,3,4 --packetsPerSource=4 --packetsLength=1024 --dataRate=1000 --vehiclesDensity=60 --seed=1 --nodesToStartInArea=2 --deltaDistance=20 --replicasPerPacket=3 --checkDataProgress=false --xmlOutput=true" > output-files/geotemporal/geotemporal_output.xml 2>&1
```

# Mobility

The ``mobility-files`` folder contains the mobility files used in NS-3 simulations. These mobility traces were created using SUMO (http://www.dlr.de/ts/en/desktopdefault.aspx/tabid-9883/16931_read-41000/). The map that the mobility traces follow is based in the city of Murcia, Spain.

The ``mobility-files`` folder must be directly under the ``/ns-allinone-X.YY/ns-X.YY`` folder (X.YY is the version of the NS-3 you are using).

There are two different mobility traces:
* Homogeneous: All the vehicle arrival points in the map have the same period between arrivals: 20, 30, 60, 90, 120, or 150 seconds between arrivals at all vehicle arrival points at once. That is, each 20 (or 30, 60, 90, 120, or 150) seconds arrives one vehicle at each arrival point.
* Heterogeneous: The north arrival points and the south arrival points have different period between arrivals, so one section of the map has more vehicles density that the other. The supplied traces are: 30-60, 30-90, 30-120, 60-90, 60-120, and 90-120. The first number indicates the arrival period for the north arrival points, the second number indicates the same for south arrival points. Both periods are measured in seconds.


# Important notes

* Given the way that NS-3 handles births and deaths of mobile nodes from SUMO mobility traces, some options about the mobility files are hard-coded in the protocol (see ``GeotemporalInstaller::Configure (int argc, char **argv)`` method from ``geotemporal/geotemporal-installer.cc``, and ``RoutingProtocol::Enable ()`` and ``RoutingProtocol::Disable ()`` methods from ``geotemporal/geotemporal-routing-protocol.cc``). 
* Not only mobility features were hard-coded, given that NS-3 is not a spatio-temporal protocol simulator, I had to take some "hard" measures (not all listed here), like writing to the output stream XML strings, to be stored in an output XML file to be able to measure some events I needed. I coded a python parser, that reads these events in XML format and computes some statistics.

For more information about NS-3 simulator visit:
* https://www.nsnam.org/
* https://www.nsnam.org/doxygen/index.html
* https://groups.google.com/forum/#!forum/ns-3-users

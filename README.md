#######################################################################
#################  PCAPNG FILE PARSER IN JAVA #########################
#######################################################################

=> http://akinaru.github.io/pcapng-java/

Update 04/05/2015

=> will parse pcap ng file with following sections  :
_ Section Header
_ Interface Description
_ Interface Statistics
_ Enhanced Packet
_ Name Resolution

Further section type will be added in the future.

-----------------------------------------------------------------------
COMMAND LINE SYNTAX : 

<b>java -jar pcapngdecoder-1.0.jar -f test.pcapng -v</b>

-f <file.pcapng> : input file
-v               : verbose, will show all section parsing content
-----------------------------------------------------------------------
PROGRAM SYNTAX :

```byte[] dataFromFile = readFile("test.pcapng");```

```PcapDecoder pcapNgDecoder = new PcapDecoder(dataFromFile);```
```pcapNgDecoder.decode();```

dont forget the import :
```import fr.bmartel.pcapdecoder.PcapDecoder```;

You will access all parsed data from pcapNgDecoder object.
A complete example is present in ```fr.bmartel.pcapdecoder.main.DisplayAllPacket``` class

getSectionList() : retrieve all sections Object

Access to section type is possible with reflection using instanceof with a set of interface defined in package fr.bmartel.pcapdecoder.structure.types.inter :

For now only 4 are parsed successfully :

* ISectionHeaderBlock
* IEnhancedPacketBlock
* IStatisticsBLock
* IDescritpionBlock
* INameResolutionBlock

A getSectionList().get(index) instanceof ISectionHeaderBlock will permit you to cast the latter interface to get access to the section's characteristics.

packet data in Enhanced Packet Block is left in packet source endianness (make it easier to compare with Wireshark result)

-------------------------------------------------------------------------

* Project is JRE 1.7 compliant
* You can build it with ant => build.xml
* Development on Eclipse 
* Specification from https://www.winpcap.org/ntar/draft/PCAP-DumpFileFormat.html
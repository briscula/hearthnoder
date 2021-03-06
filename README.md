# hearthnoder

A node.js project that logs Hearthstone TCP packet traffic and writes to files. I've only tested it on my Macbook but it should also work on Ubuntu/Linux. I'm afraid some rewriting and changes of dependencies would be needed to get it running on Windows.

## Usage:

Open a terminal in the project folder, then install the dependencies:

	$ npm install

Afterwards run `hearthnoder.js` with node.js as Superuser (sudo is required to access web traffic):

	$ sudo node hearthnoder.js

*Note:* You might need to `chown` the Dump folder recursively or change permissions if you wish to edit or delete the log files as the process is run by superuser and the log files therefore created and owned by admin.

## Making sense of the packets:

Hearthstone uses [Google Protocol Buffers](https://developers.google.com/protocol-buffers/) for network communication, which is a method of serializing structured data. To make sense of the packet data we need to get our hands on the Hearthstone `proto definition files` and then use those files to read the packets via possibly something like [protobufjs](https://www.npmjs.com/package/protobufjs).

[HearthSim/csharp-proto-extractor](https://github.com/HearthSim/csharp-proto-extractor) can be used to extract protobuf definitions from Hearthstone. Already extracted protobuf definitions using this tool are available here: [HearthSim/hs-proto](https://github.com/HearthSim/hs-proto).

## Credits

This blog post helped me alot with getting this project to work: [Heroes of Hearthstone: Capturing game packets in C#](http://www.theforce.dk/hearthstone/).

## Packet data example:

	2015-03-08 22:12:35, 1425852755541
	80.239.211.186:3724 -> 192.168.1.42:54888
	--------------------------------------------------------------
	000: 1300 0000 240c 0000 0a83 022a 8002 0a29  ....$......*...)
	001: 0801 1204 0814 1001 1204 0831 1001 1204  ...........1....
	002: 0835 1001 1205 08c6 0110 0412 0508 ca01  .5..............
	003: 1001 1205 08cc 0110 0212 6408 0112 0f08  ..........d.....
	004: c786 d1ba a580 8080 0210 bf96 9915 1800  ................
	005: 224d 0802 1204 0811 1001 1204 081b 1004  "M..............
	006: 1204 081c 100a 1204 081d 1004 1204 081e  ................
	007: 1001 1204 081f 1001 1204 0831 1001 1204  ...........1....
	008: 0832 1001 1204 0835 1002 1205 08b0 0110  .2.....5........
	009: 0a12 0508 ca01 1002 1205 0890 0210 0112  ................
	010: 6d08 0212 0c08 8080 8080 8080 8080 0210  m...............
	011: 0018 0022 5908 0312 0408 1110 0112 0408  ..."Y...........
	012: 1710 0112 0408 1810 0112 0408 1b10 2412  ..............$.
	013: 0408 1c10 0a12 0408 1d10 0412 0408 1e10  ................
	014: 0212 0408 1f10 0212 0408 3110 0112 0408  ..........1.....
	015: 3210 0212 0408 3510 0312 0508 b001 100a  2.....5.........
	016: 1205 08ca 0110 0212 0508 9002 1001 0a3a  ...............:
	017: 0a38 0804 1207 4845 524f 5f30 381a 0408  .8....HERO_08...
	018: 2d10 1e1a 0408 3110 011a 0408 3210 011a  -.....1.....2...
	019: 0408 3510 041a 0508 c901 1003 1a05 08ca  ..5.............
	020: 0110 031a 0508 cb01 1002 0a41 0a3f 0805  ...........A.?..
	021: 1207 4353 325f 3033 341a 0408 3010 021a  ..CS2_034...0...
	022: 0408 3110 011a 0408 3210 011a 0408 3510  ..1.....2.....5.
	023: 051a 0508 c901 1003 1a05 08ca 0110 0a1a  ................
	024: 0508 cb01 1002 1a05 08b9 0210 040a 260a  ..............&.
	025: 2408 0612 001a 0408 3110 021a 0408 3210  $.......1.....2.
	026: 011a 0408 3510 061a 0508 8702 1000 1a05  ....5...........
	027: 08e7 0110 000a 260a 2408 0712 001a 0408  ......&.$.......
	028: 3110 021a 0408 3210 011a 0408 3510 071a  1.....2.....5...
	029: 0508 8702 1000 1a05 08e7 0110 000a 410a  ..............A.
	030: 3f08 0812 0743 5332 5f30 3233 1a04 0830  ?....CS2_023...0
	031: 1003 1a04 0831 1003 1a04 0832 1001 1a04  .....1.....2....
	032: 0835 1008 1a05 08c9 0110 031a 0508 ca01  .5..............
	033: 1005 1a05 08cb 0110 021a 0508 8702 1002  ................
	034: 0a26 0a24 0809 1200 1a04 0831 1002 1a04  .&.$.......1....
	035: 0832 1001 1a04 0835 1009 1a05 0887 0210  .2.....5........
	036: 001a 0508 e701 1000 0a26 0a24 080a 1200  .........&.$....
	037: 1a04 0831 1002 1a04 0832 1001 1a04 0835  ...1.....2.....5
	038: 100a 1a05 0887 0210 001a 0508 e701 1000  ................
	039: 0a26 0a24 080b 1200 1a04 0831 1002 1a04  .&.$.......1....
	040: 0832 1001 1a04 0835 100b 1a05 0887 0210  .2.....5........
	041: 001a 0508 e701 1000 0a26 0a24 080c 1200  .........&.$....
	042: 1a04 0831 1002 1a04 0832 1001 1a04 0835  ...1.....2.....5
	043: 100c 1a05 0887 0210 001a 0508 e701 1000  ................
	044: 0a26 0a24 080d 1200 1a04 0831 1002 1a04  .&.$.......1....
	045: 0832 1001 1a04 0835 100d 1a05 0887 0210  .2.....5........
	046: 001a 0508 e701 1000 0a26 0a24 080e 1200  .........&.$....
	047: 1a04 0831 1002 1a04 0832 1001 1a04 0835  ...1.....2.....5
	048: 100e 1a05 0887 0210 001a 0508 e701 1000  ................
	049: 0a54 0a52 080f 1207 4558 315f 3031 351a  .T.R....EX1_015.
	050: 0408 2d10 011a 0408 2f10 011a 0408 3010  ..-...../.....0.
	051: 021a 0408 3110 031a 0408 3210 011a 0408  ....1.....2.....
	052: 3510 0f1a 0508 c901 1002 1a05 08ca 0110  5...............
	053: 041a 0508 cb01 1002 1a05 08da 0110 011a  ................
	054: 0508 8702 1003 0a46 0a44 0810 1207 4353  .......F.D....CS
	055: 325f 3230 301a 0408 2d10 071a 0408 2f10  2_200...-...../.
	056: 061a 0408 3010 061a 0408 3110 031a 0408  ....0.....1.....
	057: 3210 011a 0408 3510 101a 0508 ca01 1004  2.....5.........
	058: 1a05 08cb 0110 021a 0508 8702 1004 0a26  ...............&
	059: 0a24 0811 1200 1a04 0831 1002 1a04 0832  .$.......1.....2
	060: 1001 1a04 0835 1011 1a05 0887 0210 001a  .....5..........
	061: 0508 e701 1000 0a26 0a24 0812 1200 1a04  .......&.$......
	062: 0831 1002 1a04 0832 1001 1a04 0835 1012  .1.....2.....5..
	063: 1a05 0887 0210 001a 0508 e701 1000 0a26  ...............&
	064: 0a24 0813 1200 1a04 0831 1002 1a04 0832  .$.......1.....2
	065: 1001 1a04 0835 1013 1a05 0887 0210 001a  .....5..........
	066: 0508 e701 1000 0a26 0a24 0814 1200 1a04  .......&.$......
	067: 0831 1002 1a04 0832 1001 1a04 0835 1014  .1.....2.....5..
	068: 1a05 0887 0210 001a 0508 e701 1000 0a26  ...............&
	069: 0a24 0815 1200 1a04 0831 1002 1a04 0832  .$.......1.....2
	070: 1001 1a04 0835 1015 1a05 0887 0210 001a  .....5..........
	071: 0508 e701 1000 0a26 0a24 0816 1200 1a04  .......&.$......
	072: 0831 1002 1a04 0832 1001 1a04 0835 1016  .1.....2.....5..
	073: 1a05 0887 0210 001a 0508 e701 1000 0a26  ...............&
	074: 0a24 0817 1200 1a04 0831 1002 1a04 0832  .$.......1.....2
	075: 1001 1a04 0835 1017 1a05 0887 0210 001a  .....5..........
	076: 0508 e701 1000 0a26 0a24 0818 1200 1a04  .......&.$......
	077: 0831 1002 1a04 0832 1001 1a04 0835 1018  .1.....2.....5..
	078: 1a05 0887 0210 001a 0508 e701 1000 0a26  ...............&
	079: 0a24 0819 1200 1a04 0831 1002 1a04 0832  .$.......1.....2
	080: 1001 1a04 0835 1019 1a05 0887 0210 001a  .....5..........
	081: 0508 e701 1000 0a26 0a24 081a 1200 1a04  .......&.$......
	082: 0831 1002 1a04 0832 1001 1a04 0835 101a  .1.....2.....5..
	083: 1a05 0887 0210 001a 0508 e701 1000 0a26  ...............&
	084: 0a24 081b 1200 1a04 0831 1002 1a04 0832  .$.......1.....2
	085: 1001 1a04 0835 101b 1a05 0887 0210 001a  .....5..........
	086: 0508 e701 1000 0a46 0a44 081c 1207 4353  .......F.D....CS
	087: 325f 3230 301a 0408 2d10 071a 0408 2f10  2_200...-...../.
	088: 061a 0408 3010 061a 0408 3110 031a 0408  ....0.....1.....
	089: 3210 011a 0408 3510 1c1a 0508 ca01 1004  2.....5.........
	090: 1a05 08cb 0110 021a                      ........
	--------------------------------------------------------------

# haierV300SApi
Here's a documentation about controlling your Haeir TV on your local network.  

I Have a Haier LEU43V300S, from V300S line, I reverse enginered the local api to control my TV with my Raspberry Pi. Here the documentation.  
Feel free to implement a Javascript/Python API.

# How it works

You need to send a GET command to your Haier TV to open connection :   
&emsp;&emsp;http://\<ipOfYourTV\>:56790/dd.xml  
Header needed :  
&emsp;&emsp;Connection: Keep-alive  
&emsp;&emsp;Host: \<ipOfYourTV\>:56790  

Response :  
```<?xml version="1.0"?><root xmlns="urn:schemas-upnp-org:device-1-0" xmlns:r="urn:restful-tv-org:schemas:upnp-dd"> <specVersion> <major>1</major> <minor>0</minor> </specVersion> <device> <deviceType>urn:schemas-upnp-org:device:tvdevice:1</deviceType> <friendlyName>HHW_HAIER_70:54:b4:a6:9a:ae</friendlyName> <manufacturer> </manufacturer> <modelName>Vestel_MB130 2018</modelName> <UDN>uuid:560c0fd8-d465-44e7-872a-abec457ffbce</UDN> </device> <locale> <name>HHW_HAIER</name> <is_3D_active>0</is_3D_active> <alexa_enabled >0</alexa_enabled > <browser_type>1</browser_type> <tv_version>MB130_VESTEL</tv_version> <software_version>5.7.10.0</software_version> <mac>70:54:B4:A5:E6:0E</mac> <dial_version>2.0</dial_version> <verificationKey>213</verificationKey> <quiUI>1</quiUI> </locale></root>```

Now you can send command to your Haier tv like this :  

Post request to :  
&emsp;&emsp;http://\<ipOfYourTV\>:56789/apps/SmartCenter  
Header :  
&emsp;&emsp;Content-Type: text/plain  
Body :  
&emsp;&emsp;```<?xml version='1.0' ?><remote><key code='1012'/><?xml version='1.0' ?>``` // 1012 is the code to switch OFF TV and put in stand-by

# List of Code action
|Body|Function|
|--|--|
|```<?xml version='1.0' ?><remote><key code='1012'/><?xml version='1.0' ?>```| switch off / Send again to switch on again (note: switch on does not work when you switch off your tv with physical remote)|
|```<?xml version='1.0' ?><remote><key code='1013'/><?xml version='1.0' ?>```| mute sound|
|```<?xml version='1.0' ?><remote><key code='1016'/><?xml version='1.0' ?>```| Increase Volume|
|```<?xml version='1.0' ?><remote><key code='1017'/><?xml version='1.0' ?>```| Decrease Volume|
|```<?xml version='1.0' ?><remote><key code='1032'/><?xml version='1.0' ?>```| Next Channel|
|```<?xml version='1.0' ?><remote><key code='1033'/><?xml version='1.0' ?>```| Previous Channel|
|```<?xml version='1.0' ?><remote><key code='1034'/><?xml version='1.0' ?>```| Go Back to last Channel|
|```<?xml version='1.0' ?><remote><key code='1053'/><?xml version='1.0' ?>```| OK|
|```<?xml version='1.0' ?><remote><key code='1037'/><?xml version='1.0' ?>```| Exit|
|```<?xml version='1.0' ?><remote><key code='1010'/><?xml version='1.0' ?>```| back button|
|```<?xml version='1.0' ?><remote><key code='1048'/><?xml version='1.0' ?>```| Menu|
|```<?xml version='1.0' ?><remote><key code='1049'/><?xml version='1.0' ?>```| Pause|
|```<?xml version='1.0' ?><remote><key code='1025'/><?xml version='1.0' ?>```| Play|
|```<?xml version='1.0' ?><remote><key code='1024'/><?xml version='1.0' ?>```| Stop|
|```<?xml version='1.0' ?><remote><key code='1028'/><?xml version='1.0' ?>```| next|
|```<?xml version='1.0' ?><remote><key code='1027'/><?xml version='1.0' ?>```| previous|
|```<?xml version='1.0' ?><remote><key code='1051'/><?xml version='1.0' ?>```| record|
|```<?xml version='1.0' ?><remote><key code='1055'/><?xml version='1.0' ?>```| red|
|```<?xml version='1.0' ?><remote><key code='1054'/><?xml version='1.0' ?>```| green|
|```<?xml version='1.0' ?><remote><key code='1050'/><?xml version='1.0' ?>```| yellow|
|```<?xml version='1.0' ?><remote><key code='1052'/><?xml version='1.0' ?>```| blue|
|```<?xml version='1.0' ?><remote><key code='1062'/><?xml version='1.0' ?>```| Youtube|
|```<?xml version='1.0' ?><remote><key code='1064'/><?xml version='1.0' ?>```| netflix|
|```<?xml version='1.0' ?><remote><key code='1056'/><?xml version='1.0' ?>```| Change source (HDMI, AV, etc...) (note : send several time to change source)|
|```<?xml version='1.0' ?><remote><key code='1057'/><?xml version='1.0' ?>```| Source list too (I don't know why)|
|```<?xml version='1.0' ?><remote><key code='1001'/><?xml version='1.0' ?>```| pad Number 1000 to 1009, send 1001 for Channel 1, send 2 command like 1002 and after 1003 for channel 23|
|```<?xml version='1.0' ?><remote><key code='1009'/><?xml version='1.0' ?>```||
|```<?xml version='1.0' ?><remote><key code='1000'/><?xml version='1.0' ?>```||
|```<?xml version='1.0' ?><remote><key code='1015'/><?xml version='1.0' ?>```| Subtitle and language menu|
|```<?xml version='1.0' ?><remote><key code='1031'/><?xml version='1.0' ?>```| Activate Subtitle/Deactivate|
|```<?xml version='1.0' ?><remote><key code='1020'/><?xml version='1.0' ?>```| Arrow Up|
|```<?xml version='1.0' ?><remote><key code='1019'/><?xml version='1.0' ?>```| Arrow Dozn|
|```<?xml version='1.0' ?><remote><key code='1021'/><?xml version='1.0' ?>```| Arrow Left|
|```<?xml version='1.0' ?><remote><key code='1022'/><?xml version='1.0' ?>```| Arrow Right|
|```<?xml version='1.0' ?><remote><key code='1018'/><?xml version='1.0' ?>```| Information|
|```<?xml version='1.0' ?><remote><key code='1014'/><?xml version='1.0' ?>```| Color profile|
|```<?xml version='1.0' ?><remote><key code='1042'/><?xml version='1.0' ?>```| time to switch-off, send multiple time to change value|
|```<?xml version='1.0' ?><remote><key code='1046'/><?xml version='1.0' ?>```| Web Browser|
|```<?xml version='1.0' ?><remote><key code='1065'/><?xml version='1.0' ?>```| Web Browser (Different One?)|
|```<?xml version='1.0' ?><remote><key code='1072'/><?xml version='1.0' ?>```| Show virtual Remote with number|
|```<?xml version='1.0' ?><remote><key code='1073'/><?xml version='1.0' ?>```| Show virtual Remote with othe button|
|```<?xml version='1.0' ?><remote><key code='1040'/><?xml version='1.0' ?>```| Fav list|
|```<?xml version='1.0' ?><remote><key code='1047'/><?xml version='1.0' ?>```| Program Guide|
|```<?xml version='1.0' ?><remote><key code='1053'/><?xml version='1.0' ?>```| Show Channel List|
|```<?xml version='1.0' ?><remote><key code='1060'/><?xml version='1.0' ?>```| Teletexte (What's the name in english?)|
|```<?xml version='1.0' ?><remote><key code='1063'/><?xml version='1.0' ?>```| Channel type (Numerical, Satellite, Analogic)|
|```<?xml version='1.0' ?><remote><key code='1067'/><?xml version='1.0' ?>```| Settings|
















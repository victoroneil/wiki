This module contains functions for send and receive information through [LoRa WAN] (https://www.lora-alliance.org/What-Is-LoRa/Technology).

Lua RTOS support for LoRa WAN is build over [LMIC] (https://www.research.ibm.com/labs/zurich/ics/lrsc/lmic.html) stack from IBM. Currently only LoRa WAN class A nodes are supported in Lua RTOS (support for LoRa WAN class C nodes are scheluded to 2017 Q2).

Please, take note that build a LoRa WAN network involves a lot of things, such as the node, the gateway, the network coordinator, etc ... In this page we only talk about the node and how it is programmed, you can know more about our work on LoRa WAN in [whitecatboard.org] (http://whitecatboard.org).

# What do you need?

For use this module you need a SPI LoRa WAN transceiver, such as [RFM95] (http://www.hoperf.com/rf_transceiver/lora/RFM95W.html). Currently we are working on a board that will integrate this chip and ESP32.

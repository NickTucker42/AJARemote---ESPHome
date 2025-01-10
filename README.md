# AJARemote---ESPHome
ESPHome Template for the AJARemote

Below is a template for using ESPHome with the AJARemote hardware.  You will need a programmer inorder to install the base ESPHome firmware.


esphome:
  name: ajaremote1
  friendly_name: AJARemote1

esp32:
  board: esp32dev
  framework:
    type: arduino

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "redacted"

ota:
  - platform: esphome
    password: "redacted"

wifi:
  networks:
  - ssid: "redacted"
    password: !secret 1wifi_password
  - ssid: "redacted-2"
    password: !secret 2wifi_password 

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Ajaremote1 Fallback Hotspot"
    password: "redacted"

captive_portal:

#==================================================================
# Defined for use with the AJARemote hardware.  
#==================================================================
remote_receiver:
  pin: 
    number: GPIO15
    inverted: true

   # Change this for what ever encoding you wish.  RAW is pretty universal. 
  dump: raw
  
remote_transmitter:
  pin: 
   number: GPIO4
  carrier_duty_percent: 50%    
#==================================================================

button:

# This is using the RAW format.  Use what ever format fits your needs.  Consult the ESP Home page for details.
# Onkyo
  - platform: template
    name: Onkyo Power
    on_press:
     - remote_transmitter.transmit_raw:
        code: [8534, -4466, 585, -499, 603, -1626, 605, -499, 602, -499, 600, -1626, 603, -500, 601, -1624, 605, -1650, 581, -498, 600, -500, 599, -1627, 601, -1626, 603, -499, 600, -1625, 604, -1648, 580, -500, 599, -1649, 578, -1649, 580, -499, 599]
        carrier_frequency: 38kHz

     - remote_transmitter.transmit_raw:
        code: [-1649, 578, -500, 598, -500, 597, -1648, 578, -1649, 579, -499, 599, -499, 596, -1649, 578, -499, 597, -1648, 579, -1648, 579, -500, 597, -499, 597]
        carrier_frequency: 38kHz        
#      
  - platform: template
    name: Onkyo_Bluray
    on_press:
     - remote_transmitter.transmit_raw:
        code: [8513, -4487, 586, -499, 604, -1626, 633, -470, 602, -500, 600, -1626, 603, -500, 601, -1649, 580, -1627, 604, -499, 600, -499, 599, -1627, 602, -1627, 603, -499, 600, -1625, 603, -1625, 605, -499, 600, -499, 599, -498, 598, -1649, 579]
        carrier_frequency: 38kHz

     - remote_transmitter.transmit_raw:
        code: [-1624, 604, -499, 599, -499, 597, -500, 597, -1648, 578, -1650, 579, -1625, 603, -499, 599, -498, 596, -1650, 578, -1627, 600, -1627, 601, -499, 598]
        carrier_frequency: 38kHz  
#
  - platform: template
    name: Onkyo_Game
    on_press:
     - remote_transmitter.transmit_raw:
        code: [8448, -4489, 583, -500, 601, -1625, 604, -500, 597, -500, 597, -1625, 603, -499, 598, -1649, 579, -1649, 578, -1650, 578, -499, 598, -1648, 579, -1626, 602, -499, 598, -1648, 578, -1647, 580, -499, 597, -1650, 577, -499, 596, -1650, 576]
        carrier_frequency: 38kHz

     - remote_transmitter.transmit_raw:
        code: [-1649, 578, -500, 595, -501, 594, -500, 593, -501, 593, -499, 593, -1649, 576, -500, 594, -499, 594, -1649, 575, -1649, 577, -1649, 576, -1649, 601]
        carrier_frequency: 38kHz 
#


This is a expanded version (with imporvements) over current 4 port relay controller via Raspberry Pi using GPIO's.

Node-red flow for multi-port relay board. Designed with ver. 1.2.6, should work on older with correct palettes installed.

Requirements: Raspberry Pi (2/3B/4 or newer)
              Node-Red
              
              Palettes Required:
              
              Dashboard (node-red-dashboard v2.25.0 or newer)
                
              Dashboard LED (node-red-contrib-ui-led v0.3.3 or newer)
              
              Raspberry Pi GPIO (node-red-node-pi-gpio v1.2.3 or newer)
              
(01/01/21) Newly Added Features

  - Added API access via 'Link' from other flows that may be installed on your system, making it simple to change relay settings without messing with any code.
  
  - Added 4 different 'Trigger' events for each relay via Linked messages from other flows. 
        String 'True' / 'False', Boolean true / false, and value_above_on / value_below_on with passable threshold value. 
  
  - There was a request for a clearer looking GUI so that if only a 4 relay board was used, all 8 options would not be shown. Now, the GUI is broken into 3 parts,
      relays 1-4 in one widget, 5-8 in another, and the logging in a seperate widget. The system now automatically adjust if buttons for relay 5-8 are shown, however
      they can be forced on by the user, if so desired.
      
  -   Logging of the last 10 commands shown on the GUI is totally optional now, and can be enabled/disabled in the configuration function.
  
  -   Copy and Paste Examples of how to pass commands from another flow is included and shown at the bottom of the flow.
            * They are NOT active, and can be used in another flow and has inline documentation included. *


(12/29/20) Newly Added Features:

  - Option to restore last relay settings on startup, or return to pre-configured state.
  - Automatically save relay settings on any change to file 'relay_controller_settings.csv'
  
  - All configuration options now moved to 'Config Settings' function for easy access
  
  - GPIO Pins 29, 31-33, 35-38, and 40 are already preconfigued for use with up to 8 port relay boards.
  
  - All relays can individually be named, set for 'Low to High' or 'High to Low' relay boards
  
  - Option to disable GUI control for particular relay button(s) for limited local control, if needed. Visual status (LED) will still follow relay mode (On/Off).
  
  - Added HTTP API access.
    - 'get' all relay values (On/Off) in CSV form,
    - 'get' specific relay value
    - 'set' specific relay value
    - 'status' of all relays in human readable details information
    
    - API has no html/css markups, all output is scrapable by various programming languages for external control.
    
    - ALL relay ports are accessable via API, regardless of if GUI button is 'Disabled'.
    
    - Can accept commands from home automation controllers that can issue HTTP GET commands, such as Domoticz, to change status of relay based on external events/triggers. 
    - [TODO] Allow home automation controllers to be able to request status in a uniformed manner (json?) [TODO]
  
    - Dashboard now shows last 8 commands issued, as well as timestamp and if it was does by the [D]ashboard or by [A]PI command.
  
  

HTTP API Examples :

      http://pi_ip_address:1880/api?action=get&relay=      (Shows csv for each relay current status)
      http://pi_ip_address:1880/api?action=get&relay=1     (Shows only relay 1 current status)

      http://pi_ip_address:1880/api?action=set&relay=1&value=1     (Sets Relay 1 to 1*)
      http://pi_ip_address:1880/api?action=set&relay=1&value=0     (Sets Relay 1 to 0*)
      http://pi_ip_address:1880/api?action=set&relay=4             (Sets Relay 4 to 0)

      http://pi_ip_address:1880/api?action=status     (Shows human readable details/status of all relays)

        * value is not defined as 'On' or 'Off' to allow for L2H as well as H2L relay boards.


![alt text](https://raw.githubusercontent.com/va24531/8port_relay/main/8_port_github_flow.jpg?raw=true)







![alt text](https://raw.githubusercontent.com/va24531/8port_relay/main/8_port_github_dashboard.jpg?raw=true)

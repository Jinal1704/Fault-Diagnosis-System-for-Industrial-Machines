# Node-RED Setup and Dashboard for Temperature & Vibration Monitoring
## 1. Install Node-RED on BBB
Run the following commands to install Node-RED:
```bash
sudo apt update
sudo apt install node-red -y
```
- Start Node-RED
 ```bash
node-red
```
- By default, Node-RED runs on port 1880 0r 1881.
- Open http://BBB_IP_ADDRESS:1880  or  http://BBB_IP_ADDRESS:1881 in a web browser.

## 2. Install Node-RED Dashboard
In the Node-RED UI, open the Manage Palette (Menu > Manage Palette):
- Click on the Install tab.
- Search for node-red-dashboard and install it.

## 3. Create Node-RED Flow for Sensors Data
1. **Add an MQTT Input Nodes**
   - Drag two MQTT in nodes from network section.
   - Double-click the first MQTT in node:
     - **Server**: `localhost:1883` (since Mosquitto runs on BBB)
     - **Topic**: ` sensor/vibration`
     - **QoS**: 0
     - **Output**: String
     - Click **Done**
    - Double-click the second MQTT in node:
      - **Server**: `localhost:1883` (since Mosquitto runs on BBB)
      - **Topic**: ` sensor/temperature`
      - **QoS**: 0
      - **Output**: String
      - Click **Done**
2. **Add a JSON Node**
   - Drag a  2 json node and connect it to the MQTTs node.
   - This converts the received MQTT message to a readable format.
3. **Add a Gauge Node**  
   - Drag a `Gauge` node from the Dashboard section.
     - For Temperature:
       - Drag a Gauge node from dashboard
       - Double-click:
         - Group: Your Dashboard Group
         - Label: Temperature
         - Min: 0
         - Click Done.
       - Connect it to the JSON node.
     -  For Vibration:
       - Drag another Gauge node.
       - Configure similarly with:
         - Label: Vibration Level
         - Min: 0
         - Max: 1023
       - Connect it to the JSON node.

 ### for UI Group
 1. Open Node-RED Dashboard Settings
    - Click on the ☰ (menu) in the top-right corner.
    - Select "Dashboard" from the dropdown menu.
 2. Go to the "Layout" Tab
    - In the Dashboard settings window, you will see different tabs:
      - Layout
      - Site
      - Theme
      - Settings
    - Click on the "Layout" tab.
 3. Check for Existing Groups
    - Under "Layout", you should see Tabs and Groups listed.
    - If no groups exist, you need to create a new group.
 4. Create a New Group (If Needed)
    - Click "Add a new tab" (if no tab exists).
    - Click "Add a new group" inside the tab.
    - Assign your UI nodes (like "vibration level") to this group.
   
  ## 4.Deploy and Test
   - Click Deploy.
   - Open http://BBB_IP_ADDRESS:1880/ui or http://BBB_IP_ADDRESS:1881/ui to see the dashboard.

       
   




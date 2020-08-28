# TPLinkEAP225
TPLink EAP225 SSH custom component for Home assistant for detecting mac addresses

With this custom component, you'll be able to detect a single MAC address in a TPLInk EAP225 access point.

Here are the steps:

First, you need to log in the EAP225 and create an SSH access (Management - SSH - port: 22, enable)

Then, copy the custom_component in your Home Assistant Config subdirectory (the directory where configuration.yaml is)

You need to have a subdirectory named "custom_components" and in this subdirectory, create eap225 and in this eap225 subdirectory, copy the files

Then, in configuration.yaml, add the following:
```
eap225:
  # host is the ip of the EAP225 access point
  host: 192.168.3.4
  # then you need to provide username and password to log into it (the same credentials you used in the web interface)
  username: abcdefg
  password: hijklm
  # finally a list of interfaces to query. Normally ath0 is the first 2.4ghz interface, ath1 is the second, etc and ath10 is the first 5ghz interface
  interfaces:
  - ath0
  - ath1
  - ath10
```

Then, in your binary sensors (either the binary_sensors: section of configuration.yaml or your binary_sensors.yaml file)
```
binary_sensor:
  - platform: eap225 
    name: presence_mac1
    # make sure the mac address is lowercase and separated with :
    mac: aa:bb:cc:dd:ee:ff
```
Then restart home assistant, and you should have a new binary sensor named presence_mac1 that will follow the presence of this mac address on the eap225
You can create as many binary sensors as you want to follow different mac addresses.

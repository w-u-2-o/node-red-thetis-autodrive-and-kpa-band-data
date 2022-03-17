# node-red-thetis-autodrive-and-kpa-band-data

 A Windows Node Red flow to implement autodrive and KPA amplifier band data controls
 
 AUTODRIVE
 
 "Autodrive" is a concept originally devised by the author of DDUtil, whereby the radio drive level is automatically set on a band by band basis to the a user specified level for driving an amplifier. While Thetis does remember the last set drive level per band in the band stack registers, if these are changed it's easy to lose track of where you really want them.
 
 Every time you change bands with autodrive enabled, the user specified drive level is reasserted in Thetis.
 
 This autodrive implementation is quite thorough. It checks the state of split, RX1, RX2, VFOA and VFOB in Thetis to determine the actual TX band.
 
 It also has a feature whereby it will automatically cutback drive levels by a certain percentage when either DIGU or DIGL are selected as the TX mode. Again it is very thorough and determines actual TX mode, not just whata is in VFOA.
 
 KPA BAND DATA
 
 The TX band that is carefully determined as described above is encoded into a KPA1500 compatible CAT command and sent via a Node Red link-out/link-in connection to the companion KPA1500 control flow for automatic amplifier band switching.
 
 FLOWS
  
 There are two flows, one for the actual control and UI, and the other for setup.
 
 Control & UI flow:
 
 The Control UI is quite simple. There is a setup button, a button to enable/disable autodrive, a display of the currently commanded autodrive level, and a button to reset Thetis to that level if you've moved off of it manually in Thetis. That's a little slicker than moving to another band and back again.
 
 There are no controls or UI for KPA band data. The KPA will display the band it is set to, as does Thetis.
 
 Setup flow:
 
 The setup flow allows the operator to define the Thetis IP and port addresses, and fill out a table of autodrive levels by band, including a value for digital mode power cutback from those levels in percent.
 
 Thetis network settings are saved in c:\node-red\thetis_settings.json, and autodrive levels are saved in c:\node-red\autodrive_settings.json. The directory will be created if it is missing.
  
 Developed under node 16.12.0 and npm 8.1.0.
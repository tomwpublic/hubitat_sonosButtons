# hubitat_sonosButtons

This provides a user-friendly interface into Hubitat for the extremely useful node-sonos-http-api:  https://github.com/jishi/node-sonos-http-api

Basic grouping and ungrouping functionality are provided as custom commands.  The PushableButton interface is used as a quick way of providing any custom action without having to create complicated rules or custom drivers to make the specific HTTP accesses to the API.  There is also functionality for displaying album art if it is available from your audio source.

This library is intended as a companion to the built-in Sonos integration and can be used alongside it.

# Installation instructions:

* Install the node-sonos-http-api on your external server of choice and ensure that it is working correctly: https://github.com/jishi/node-sonos-http-api/blob/master/README.md
* In the *Drivers Code* section of Hubitat, add the sonosButtonsSystem and sonosButtons drivers.
* In the *Devices* section of Hubitat, *Add Virtual Device* of type Sonos Buttons System.  Enter the IP and MAC addresses of your **node server** (note: this is not the same as any of the Sonos speakers) and click *Save Preferences.*
* If you want real-time updates (without polling), set up the webhook functionality as described in the node-sonos-http-api readme.  Set the webhook entry in your settings.json as `{ "webhook" : "http://<your hub IP>:39501" }`
    * Otherwise, you can poll for updates by executing the Refresh command on the Sonos Buttons System device.
* Add Sonos Buttons devices using the *addChildSpeaker* command for any speakers that you want to control.

# Usage instructions:

* **Join and Leave**

    * *Join* will join this speaker to whichever speaker is specified in master.  Note that this can typically be any other speaker, whether it is currently grouped or not.  If master is currently grouped, this speaker will be added to the same group.
    * *Leave* will cause this speaker to leave any group that it is a part of.

* ***Push* operations**

    * Numbered buttons are mapped to saved HTTP commands to the node server and are executed when pressed.  See below for instructions on creating custom commands.  Saved commands appear in the *buttonMap* entry on the device page.
    * The sonosButtons driver code also demonstrates how to enter default behaviors at the driver source code level for numbered buttons that do not have a custom command associated.  Inspect the *push(buttonNumber)* command for examples.

* **Creating custom button commands**

    * Visit the node-sonos-http-api command reference page for ideas.  This can be found at `http://<node IP>:<node port>` in a web browser.
    * And commands from the *Zone Control* section can be saved as number buttons in a sonosButtons device.  Use the *addButton* command as described here:
        * Enter the desired button number to use.
        * Enter the fully command string, beginning from the portion after `{zone name}/` in the command reference.  For example, entering `mute` (no leading slash) will execute the `/{zone name}/mute` command on this zone.

* **Album art attributes**

    * albumArtDisplay and albumArtUri attributes are populated if they are available for the media source.
        * You can use albumArtDisplay in a dashboard Attribute tile.
        * You can use albumArtUri as a direct URI to the album art.



# Disclaimer

I have no affiliation with any of the companies mentioned in this readme or in the code.



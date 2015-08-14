# hidclient
fork of Anselm Martin Hoffmeister's [hidclient](http://anselm.hoffmeister.be/computer/hidclient/index.html.en)

hidclient is a Virtual Bluetooth® keyboard and mouse

**What is this about?**

The hidclient program makes a Bluetooth® technology equipped computer appear as a Bluetooth® keyboard and mouse device to other machines. Input events (like keystrokes and mouse movements) of the locally attached input devices will be forwarded to another machine via the Bluetooth® link.
For the counterpart (which might be a Linux PC, a Win PC, a PDA...) there is no technical difference to "real" Bluetooth® input devices.

**What will I need?**

A Linux PC (or laptop, possibly a PDA would do...?) that runs the Bluez Software.
Most distributions should supply this.
A Bluetooth® dongle (USB-Stick...) for this machine
Another device that is able to handle Bluetooth® input devices: A PC, PDA or similar (not necessarily running Linux!)
The bluez header files (for compiling the sources)
The hidclient source code (see below).

**What am I allowed to do with this program?**

Well, you may use it, read the source code, give the files to other people, change it - basically anything provided you stay within the limits of the GNU General Public License version 2 (or any later version, at your choice).
This program is "free software" (both as in speech and in beer), you do not need to pay any royalties for using it. Keep with the GPL.

**Build**

hidclient depends on `libbluetooth` from bluez.

Compile hidclient.c with

    gcc -o hidclient -O2 -lbluetooth -Wall hidclient.c
    
You don't need to copy anything into `/etc/bluetooth`. Might be a good idea to edit `/etc/bluetooth/main.conf` and set `DisabledPlugins=input` there, and `Class=0x000540` - that helps identifying the device as a "keyboard".
Now run

    sudo ./hidclient -l
    
to list the available input devices. If you have for example two usb mice and want to export only one (while working locally on the other), select the ID number from the first column.
Start hidclient with

    sudo ./hidclient -e4 -x
    
where 4 is the number of your mouse. Hidclient will wait for bluetooth connections. The mouse should stop working on the local PC, so it will not interfere with your normal computer usage while it is connected to another device.

Use `openvt` along with hidclient so that keystrokes and mouse events captured will have no negative impact on the local machine (except Ctrl+Alt+[Fn/Entf/Pause]).
Run

    openvt -s -w hidclient
    
 to run hidclient on a virtual text mode console for itself.

Or use `-x`, will "mute" the device(s) for X11 so you can start hidclient while having a X11 session.

With the `-x` parameter, you can ignore the `openvt` mentioned above.


The word trademark Bluetooth® is a registered trademark of the [Bluetooth SIG](http://www.bluetooth.org).

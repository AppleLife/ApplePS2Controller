ApplePS2Controller
==================

Apple provides the source code for the PS/2 controller driver as well as the code for the mouse, keyboard, and trackpad drivers.

When using this code you'll see that the AppleACPIPlatfromExpert will provide the two nubs (IOACPIPlatformDevice instances) which the above AppleACPIPS2Nub class will attach to. That class itself is a nub which ApplePS2Controller will attach to. The ApplePS2Controller class then provides two nubs (ApplePS2KeyboardDevice and ApplePS2MouseDevice) which the drivers in the ApplePS2Keyboard and ApplePS2Mouse kernel extensions will then attach to.

You can view all of this using ioreg -w0. If you want to see how the interrupt controllers/specifiers properties work you may want to add the -l flag.

Note that ApplePS2Controller drives the controller (so it's a driver) but it also provides a nub that the mouse and keyboard drivers can attach to. Therefore, you'll also need the mouse and keyboard drivers.

Now, a possible alternative implementation would be to instead create subclasses of ApplePS2KeyboardDevice and ApplePS2MouseDevice which attach directly and independently to the ACPI nubs instead of to the PS2 controller. On the other hand, it is classically modeled as one device, not two independent devices and doing it this way would prevent common code in ApplePS2Controller from driving the controller as one device.

# avkans-visca-utils

Visca over TCP control for AVKans E20 Cameras, and probably other AvKans or PTZOptics cameras.

This package is really intended for the E20 NDI camera, and includes computations based on it's geometry and speed characterizations.   It was originally created to allow for real-time AI camera functionality via Python.

This package is not distributed by or endorsed by AVKans.

## License
This package is licensed under the "MIT License" - See license.txt

## Example Usage

```
from avkans-visca-utils import AvkansControl

# Connect over TCP
cam1 = AvkansControl("192.168.100.110")

# Go to +45,+20 position at full speed.
print("Going to 45,20")
cam1.send_raw(cam1.cmd.ptz_to_abs_position(45,20,1,1))
cam1.wait_complete()

# Set zoom level at 50% - 10x zoom for Avkans E20
print("Zoom 50%")
cam1.send_raw(cam1.cmd.zoom_set_position(0.5))
cam1.wait_complete()

# Implement a continuous servo loop
while(True):
  cmd_vector = [do your inference here with Yolo, etc]
  cam1.send_raw(cam1.cmd.ptz_to_abs_position(cmd_vector))

```


AVKans makes a line of affordable NDI cameras that work very well, but the visca / TCP controls are a bit quirky.

This library is specifically targeted at the inexpensive E20 cameras, but should work with most of the Avkans or PTZ Optics lineup.

# Setup and use

Run commands from the repository root. The code targets the Arduino and Raspberry Pi setup used in the course project. Match the wiring and serial settings to your robot before running it.

## Python and camera

```sh
pip install opencv-python numpy pyserial
python dialogue.py
```

Tkinter is needed for the interface. The hardware camera code uses the legacy `picamera` API on a Raspberry Pi. Without it, the interface can open but there is no live camera feed. The supplied code does not implement a generic USB-webcam backend.

`dialogue.py` starts the interface in `menu_ui.py`. It has serial connection settings, camera controls, manual commands, line following and route planning. The CLI menu can also be opened with:

```sh
python -c "from dialogue import run_cli_menu; run_cli_menu()"
```

## Arduino

1. Open `serial_link.ino` in Arduino IDE, with `parameters.h` alongside it.
2. Check the board, wiring and pin assignments in `parameters.h`.
3. Upload the sketch and select its serial port in the Python interface. The supplied baud rate is 115200.

The firmware handles motor commands and sensor readings. `parameters.h` defines the motor, infrared and other hardware pins.

## Code and model

- `dialogue.py`: serial communication, camera capture, line following and route planning.
- `menu_ui.py`: Tkinter controls and track view.
- `intersections.py`: intersection detection.
- `infrared_utils.py`: infrared distance measurements.
- `serial_link.ino` and `parameters.h`: Arduino firmware and hardware settings.
- `suivi_ligne_huit_eleve_2022b.slx`: the Simulink model.
- `huit.jpg` and `huit_obstacle.jpg`: track images.

For camera tuning, see `resolution_target` and `init_camera()` in `dialogue.py`. Steering gains are in `compute_steering_command()`; intersection thresholds are in `intersections.py`. The presentation linked from the README explains the group project.

## Troubleshooting

Check the serial port and baud rate if the Arduino does not answer. On Linux, serial-device permissions may need configuring. If line following is unstable, check lighting, camera framing, detection thresholds and steering gains against the actual track.

## Original project notice

Copyright (c) 2025 CentraleSupélec. Educational use permitted with attribution.

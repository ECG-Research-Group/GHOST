# Operation and software setup

Follow this guide after completing [hardware assembly and connections](assembly.md). It covers controller software setup, motion verification, calibration, and recording measurements during fish-tail lifts.

The GHOST controller software runs on the Raspberry Pi. Use the same laptop for both remote control and data recording:

| Software                  | Runs on        | Purpose                                                           |
| ------------------------- | -------------- | ----------------------------------------------------------------- |
| GHOST controller software | Raspberry Pi 4 | Configure and control the lifting sequence.                       |
| RealVNC Viewer            | Laptop         | View the Raspberry Pi desktop and operate GHOST remotely.         |
| LabChart                  | Laptop         | Display, record, and save measurements acquired through PowerLab. |


## Before setup

The controller software and GHOST system image are not included in this repository. Obtain them and their verified installation instructions from the project team before proceeding; see [controller software status](../software/README.md). The steps below depend on those materials and the configuration of the recovered image.

## 1. Configure the Wi-Fi hotspot

1. Open the router's administration by entering in the browser: `192.168.0.1`.
2. Set the hotspot credentials exactly as shown below, then save the settings.

   | Hotspot setting     | Value       |
   | ------------------- | ----------- |
   | Network name (SSID) | `GHOST-2.4` |
   | Wi-Fi password      | `GHOST2024` |

3. Connect the laptop to `GHOST-2.4` using this password.

The network name is the hotspot's SSID. Router administration and Raspberry Pi/VNC sign-in use their own credentials.

## 2. Prepare the Raspberry Pi 4 microSD card

1. Obtain the GHOST system image and its installation instructions from the project team. Record the image and controller software versions.
2. Insert the microSD card into the laptop's card reader.
3. Follow the verified image-writing instructions to select the GHOST system image and destination microSD card, write and verify the image, and safely eject the card.
4. With the Raspberry Pi powered off, insert the prepared microSD card, then power on the Pi.
5. Follow the image's first-boot instructions, if required, and confirm that the Pi joins `GHOST-2.4`. Check the router's connected-device list for the Pi's IP address and record it for the next step.

**Check:** The Raspberry Pi and laptop are connected to the same network, and you have the Pi's current IP address.

## 3. Connect to the Raspberry Pi with RealVNC

1. Download and install [RealVNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) on the laptop, using a version compatible with the supplied image.
2. Open RealVNC Viewer and enter the Raspberry Pi's IP address to connect.
3. Sign in with the Raspberry Pi/VNC credentials supplied with the image.
4. Confirm that the Raspberry Pi desktop is visible and responds to the laptop's mouse and keyboard.

The Pi must have a compatible VNC server enabled for this connection. Use the project's image-specific instructions if it cannot be reached; see [RealVNC connection basics](https://help.realvnc.com/hc/en-us/articles/38538874117533-RealVNC-Viewer-and-Server-Basics) for general guidance.

## 4. Open LabChart and check acquisition

1. Open LabChart on the laptop connected during assembly and check that PowerLab is detected.
2. Confirm that the displayed channels match the labels and channel map recorded during assembly.
3. Confirm the acquisition settings and units against the study protocol.

## 5. Configure GHOST, verify motion, and calibrate

1. Open the GHOST controller software on the Raspberry Pi desktop through RealVNC.
2. Configure and verify motor-control board addresses and channel assignments using the recovered installation instructions and the wiring record.
3. Set the study's lift parameters. The intended interval between lifts is **one hour**; other motion settings must come from the approved protocol.
4. Test without a specimen, using restricted travel. Verify direction, reference position, travel limits, return behavior, and fault response before testing a full stroke.
5. Calibrate each channel with a known weight using the [calibration plan](calibration.md). Check the readings in LabChart and save your settings.
6. Record the calibration results, channel, hardware and controller software revisions, reviewer, and date before collecting experimental data.

## 6. Start a run and monitor measurements

1. Record the run details and verify a complete cycle without a specimen before each run.
2. Attach the fish tails to the hooks according to your experimental protocol.
3. Start recording in LabChart, then start the lifting sequence in GHOST.
4. Watch the LabChart traces to see how the measured lifting load changes over time. Note the specimen ID and start time for each channel, and record errors or deviations during the run.

## 7. Stop, save, and shut down

1. Stop the GHOST sequence and make sure the mechanism is in a safe position before removing the fish. Stop the run early if motion or readings look wrong.
2. Stop recording in LabChart, preserve the raw acquisition files and run notes, and back up the files.
3. Shut down the Raspberry Pi from its desktop before disconnecting power, then clean the equipment.

## Troubleshooting

| Problem                                                    | Check                                                                                                                                                                       |
| ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Raspberry Pi does not appear on the network                | Confirm the supplied image was written and verified, the Pi has booted, and its Wi-Fi settings match `GHOST-2.4` / `GHOST2024`. Follow the image's first-boot instructions. |
| RealVNC cannot connect                                     | Confirm both devices are on the same network, check the Pi's current IP address, and verify that the image's VNC server is enabled and accepts local connections.           |
| RealVNC rejects the login                                  | Use the Pi/VNC credentials supplied with the image. The Wi-Fi password is used to join the network.                                                                         |
| PowerLab is not detected in LabChart                       | Check PowerLab power and its connection to the laptop, then follow the model-specific setup instructions.                                                                   |
| A channel is flat, clipped, or gives an unexpected reading | Check channel mapping, amplifier connections, input range, units, and calibration against the verified setup. Stop the run before changing wiring.                          |

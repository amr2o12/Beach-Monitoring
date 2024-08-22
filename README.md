# Beach Environmental Monitoring with Raspberry Pi

This project utilizes a Raspberry Pi and camera module to monitor environmental conditions on beaches. It identifies and classifies objects like trash, beachgoers, animals, and potentially hazardous items, providing real-time insights into beach health and safety.

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/) 
[![Powered by Raspberry Pi](https://img.shields.io/badge/Powered%20by-Raspberry%20Pi-orange.svg)](https://www.raspberrypi.org/)
[![Topic: Computer Vision](https://img.shields.io/badge/Topic-Computer%20Vision-yellowgreen)](https://en.wikipedia.org/wiki/Computer_vision) 

## Demo Video

This is a Demstration of an image of a shark (NOT in the training dataset)
- [AI Beach Watchdog in Action](https://youtube.com/shorts/TX7l_Vdimso)

## Features

- **Real-time Object Detection:** Continuously captures images and uses a deep learning model to detect and classify objects on the beach.
- **Environmental Monitoring:** Identifies presence of dangerous/harmful sea creatures or unusual animal activity.
- **Customizable Alerts:**  Can be configured to trigger alerts based on specific object detections, such as sending notifications when trash levels are high.
- **Data Collection and Analysis:**  Potentially store detection data for future analysis, helping understand trends and patterns in beach usage and environmental conditions.

## Hardware Requirements

* Raspberry Pi (Model 4B or newer recommended)
* Raspberry Pi Camera Module v1 (or compatible)
* Power Supply for Raspberry Pi
* SD Card (16GB or larger)
* (Optional) Case for outdoor protection

## Software Requirements

* Raspberry Pi OS (Bullseye or newer recommended)
* Python 3.7 or later
* The following Python packages:
    * `numpy`
    * `matplotlib` (optional, for development)
    * `pandas` (optional, for development) 
    * `torch`
    * `torchvision`
    * `pillow`
    * `albumentations`
    * `scikit-learn` 
    * `imutils`
    * `split-folders`
    * `textwrap3`
    * `super-gradients`
    * `pyOpenSSL`
    * `markupsafe==2.0.1` 
    * `gtts` (for text-to-speech, optional) 
    * `pygame` (for sound playback, optional)

## Installation

1. **Enable Camera and Legacy Support:**
   - Open Raspberry Pi Configuration: `sudo raspi-config`
   - Go to "Interfaces" -> "Enable Legacy Camera Support" 
   - Reboot your Raspberry Pi: `sudo reboot`

2. **Configure Camera Settings:**
   - Open the `config.txt` file: `sudo nano /boot/config.txt`
   - Add the following lines (adjust if needed):
     ```
     dtoverlay=imx219
     start_x=1
     gpu_mem=128
     dtoverlay=ov5647
     ```
   - Save and close the file.

3. **Install Snapd and CMake:**
   - Update your package lists: `sudo apt update`
   - Install Snapd: `sudo apt install snapd`
   - Reboot your Pi: `sudo reboot`
   - Install CMake: `sudo snap install cmake --channel=3.22/stable --classic` 

4. **Install Python Packages:**
   - Install required packages: `pip install -r requirements.txt`
   - (You'll need a `requirements.txt` file containing the packages listed in "Software Requirements") 

5. **Configure Audio (Optional):**
   - If you want audio feedback, install mpg123: `sudo apt install mpg123`
   - Modify `/etc/asound.conf` (create if it doesn't exist) to set your audio output device:
     ```
     pcm.!default{
         type hw
         card 1 
     }
     ```

6. **Create and Configure Systemd Service (Optional):**
   - For automatic startup, create a service file: `sudo nano /etc/systemd/system/myapp.service`
   - Paste the service configuration, modifying paths as needed:
     ```
     [Unit]
     Description=Beach Monitoring Service
     After=network-online.target

     [Service]
     Environment=DISPLAY=:0
     Environment=XAUTHORITY=/home/pi/.Xauthority
     Type=simple
     User=pi 
     WorkingDirectory=/home/pi/Desktop/your-project-folder 
     ExecStart=/usr/bin/python3 /home/pi/Desktop/your-project-folder/model_rpi_test.py
     Restart=always
     StandardOutput=syslog
     StandardError=syslog

     [Install]
     WantedBy=multi-user.target 
     ```
   - Enable and start the service:
     ```bash
     sudo systemctl enable myapp.service
     sudo systemctl start myapp.service
     ```
   - Check the service status: `sudo journalctl -u myapp.service`

7. **Download the Pre-trained Model:**
   - Download the model checkpoint file (`ckpt_best.pth`) and place it in the `model` directory within your project folder.

## Usage

1. **Connect your Raspberry Pi Camera.**
2. **Navigate to the project directory:** `cd /path/to/your/project`
3. **Run the main script:** `python3 model_rpi_test.py` 

## Project Structure
Use code with caution.
Markdown
beach-monitoring/
├── model/
│ └── ckpt_best.pth # Pre-trained model checkpoint
├── photos/ # Directory to store captured images
├── voice/ # Directory for audio files (if using audio alerts)
└── model_rpi_test.py # Main Python script
## Customization

###  Configure Object Classes and Alert Logic:

   - **Open `model_rpi_test.py` in a text editor:**
     ```python
     class_names = ['Trash', 'Beach Umbrella', 'Person', 'Seagull', 'Dog']  # Update with your classes

     friendly_fire = ['Beach Umbrella', 'Person', 'Seagull'] # Objects not considered alerts
     enemy_fire = ['Trash', 'Dog'] # Objects to trigger alerts 
     ```
   - **Modify `class_names`:** Replace with the specific object names your model is trained to recognize.
   - **Adjust `friendly_fire` and `enemy_fire`:**  Categorize objects for alert logic (what requires notification). 



## License

This project is licensed under the MIT License.

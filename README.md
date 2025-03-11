<h1 align="center" id="title">SafeSpark</h1>

<p align="center">
  <img src="https://socialify.git.ci/mohammad1388f/SafeSpark/image?language=1&amp;owner=1&amp;name=1&amp;stargazers=1&amp;theme=Light" alt="project-image">
</p>

<p id="description">
  A smart IoT-controlled ESP32-based system for safely triggering fireworks from a distance.
</p>

<h2>Table of Contents</h2>
<ul>
  <li><a href="#features">Features</a></li>
  <li><a href="#prerequisites-installation">Prerequisites &amp; Installation</a></li>
  <li><a href="#hardware-assembly-wiring">Hardware Assembly &amp; Wiring</a></li>
  <li><a href="#software-setup-flashing">Software Setup &amp; Flashing</a></li>
  <li><a href="#usage-guide">Usage Guide</a></li>
  <li><a href="#video-tutorial">Video Tutorial</a></li>
  <li><a href="#code">Code</a></li>
  <li><a href="#contribution">Contribution</a></li>
  <li><a href="#contact">Contact &amp; About the Developer</a></li>
  <li><a href="#license">License</a></li>
</ul>

<h2 id="features">Features</h2>
<ul>
  <li>
    <strong>Remote Fireworks Triggering:</strong>
    Control fireworks safely from a distance using an IoT-enabled ESP32 platform.
  </li>
  <li>
    <strong>Dynamic Countdown Timer:</strong>
    An adjustable countdown timer that initiates a series of visual and audio cues, building up anticipation before activation.
  </li>
  <li>
    <strong>Interactive Web Interface:</strong>
    A responsive HTML/CSS/JavaScript web page that allows you to start the countdown and adjust settings in real-time.
  </li>
  <li>
    <strong>Vivid LED Visual Effects:</strong>
    <ul>
      <li>
        <em>Neopixel Ring:</em> Enjoy a default continuous rainbow effect that transitions into dynamic, flashing colors during the countdown and final activation phases.
      </li>
    </ul>
  </li>
  <li>
    <strong>Customizable Audio Feedback:</strong>
    An integrated buzzer delivers an audible countdown with varying intervals, intensifying as the detonation nears.
  </li>
  <li>
    <strong>Persistent Configuration Storage:</strong>
    EEPROM integration stores user-defined settings such as the countdown duration, LED delay, and LED on-time, ensuring your preferences are retained across resets.
  </li>
  <li>
    <strong>Non-Blocking LED Updates:</strong>
    Efficient Neopixel animations maintain smooth visual effects without interrupting the countdown or other system processes.
  </li>
  <li>
    <strong>Dedicated WiFi Access Point:</strong>
    Operates as its own access point (default credentials: <code>BOOM/12345678</code>) for secure and isolated control of the system.
  </li>
</ul>

<h2 id="prerequisites-installation">Prerequisites &amp; Installation</h2>
<ul>
  <li>
    <strong>ESPRESSIF Flash Download Tools:</strong>
    <a href="https://docs.espressif.com/projects/esp-test-tools/en/latest/esp32/production_stage/tools/flash_download_tool.html" target="_blank">Download here</a>
    <img src="https://www.espressif.com/sites/all/themes/espressif/images/logo-guidelines/primary-vertical-logo.png" alt="ESPRESSIF Logo" style="height:50px; vertical-align: bottom;">
  </li>
  <li>
    <strong>Arduino IDE:</strong>
    <a href="https://www.arduino.cc/en/software" target="_blank">Download Arduino IDE</a>
    <img src="https://www.arduino.cc/wiki/370832ed4114dd35d498f2f449b4781e/arduino.svg" alt="Arduino Logo" style="height:50px; vertical-align: bottom;">
  </li>
  <li>
    <strong>ESP32 Board Package:</strong>
    Install the ESP32 board package from within the Arduino IDE.
    <img src="https://www.espressif.com/sites/all/themes/espressif/images/logo-guidelines/primary-vertical-logo.png" alt="ESPRESSIF Logo" style="height:50px; vertical-align: bottom;">
  </li>
  <li>
    <strong>Required Libraries:</strong>
    <ul>
      <li>
        <code>Adafruit_NeoPixel.h</code> – Install via the Arduino Library Manager or from 
        <a href="https://www.adafruit.com/" target="_blank">Adafruit</a>
        <img src="https://cdn-shop.adafruit.com/static/adafruit_favicon.svg" alt="Adafruit Logo" style="height:50px; vertical-align: bottom;">
      </li>
    </ul>
  </li>
  <li>
    <strong>Hardware Components:</strong>
    <ul>
      <li>DOIT ESP32 DevKit V1</li>
      <li>16-LED RGB WS2812 Neopixel Ring</li>
      <li>5V Relay Module</li>
      <li>5V Buzzer</li>
      <li>Two PC817 Optocouplers</li>
      <li>Tengestan spring with a suitable resistor (for firework fuse activation)</li>
      <li>Wires for connections and an enclosure for the device</li>
      <li>5V Power Supply or Battery</li>
      <li>Additional Power Supply or Battery with appropriate voltage for the Tengestan spring</li>
    </ul>
  </li>
</ul>

<h2 id="hardware-assembly-wiring">Hardware Assembly &amp; Wiring</h2>

<h3>Neopixel Connections</h3>
<p>Refer to <strong>Slide1.PNG</strong> for the Neopixel wiring:</p>
<ul>
  <li><strong>GND</strong> &rarr; GND</li>
  <li><strong>5V</strong> &rarr; Positive terminal of the 5V battery or power supply</li>
  <li><strong>DI</strong> &rarr; Pin D4 on ESP32</li>
</ul>
<p>
  <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/schematic/Slide1.PNG?raw=true" alt="Neopixel Connections (Slide1.PNG)" style="max-width:600px;">
</p>

<h3>Relay Connections</h3>
<p>Refer to <strong>Slide2.PNG</strong> for the relay wiring:</p>
<ul>
  <li><strong>GND</strong> &rarr; GND</li>
  <li><strong>VCC</strong> &rarr; Positive terminal of the 5V battery or power supply</li>
  <li><strong>COM</strong> &rarr; Wire from the relay connected to one end of the Tengestan spring</li>
  <li><strong>NO</strong> &rarr; The other end of the Tengestan spring</li>
</ul>
<p>
  <strong>Additional Notes for Relay Circuit:</strong>
  <ul>
    <li>
      Relay's <strong>IN</strong> pin connects to the emitter of a PC817 optocoupler.
    </li>
    <li>
      The collector of the optocoupler connects to GND or +5V (depending on your relay module).
    </li>
    <li>
      The cathode of the optocoupler goes to GND, and the anode connects to Pin D2 on the ESP32.
    </li>
    <li>
      It is recommended to use separate power supplies for the Tengestan spring and the ESP32 board.
    </li>
    <li>
      The Tengestan spring is used for activating the firework fuse.
    </li>
  </ul>
</p>
<p>
  <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/schematic/Slide2.PNG?raw=true" alt="Relay Connections (Slide2.PNG)" style="max-width:600px;">
</p>

<h3>Buzzer Connections</h3>
<p>Refer to <strong>Slide3.PNG</strong> for the buzzer wiring:</p>
<ul>
  <li>Buzzer cathode &rarr; GND</li>
  <li>Optocoupler cathode &rarr; GND</li>
  <li>Buzzer anode &rarr; Emitter of the optocoupler</li>
  <li>Collector of the optocoupler &rarr; +5V</li>
  <li>Optocoupler anode &rarr; Pin D15 on ESP32</li>
</ul>
<p>
  <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/schematic/Slide3.PNG?raw=true" alt="Buzzer Connections (Slide3.PNG)" style="max-width:600px;">
</p>

<h3>Summary of Connections</h3>
<p>Overview of wiring to the DOIT ESP32 DevKit V1 is shown in <strong>Slide4.PNG</strong>:</p>
<p>
  <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/schematic/Slide4.PNG?raw=true" alt="Summary of Connections (Slide4.PNG)" style="max-width:600px;">
</p>

<h3>Enclosure Example</h3>
<p>After completing the assembly, you can mount everything in an enclosure as demonstrated in <strong>Slide5.PNG</strong>:</p>
<p>
  <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/schematic/Slide5.jpg?raw=true" alt="Enclosure Example (Slide5.jpg)" style="max-width:600px;">
</p>

<h2 id="software-setup-flashing">Software Setup &amp; Flashing</h2>

<h3>ESPRESSIF Flash Download Tools</h3>
<p>
  The ESPRESSIF Flash Download Tools is used to upload the binary file to the ESP32. It is fast and requires no special installation or configuration (its settings cannot be modified). The download link is provided in the <em>Prerequisites &amp; Installation</em> section.
</p>
<p>Installation Steps:</p>
<ol>
  <li>
    Open the Flash Download Tools. The initial screen (shown below) allows you to select the target board.
    <br>
    <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/Software%20Settings/Slide2.png?raw=true" alt="ESPRESSIF Flash Download Tools - Board Selection" style="max-width:600px;">
  </li>
  <li>
    For version 2.0, which is developed exclusively for the ESP32, set the <strong>workmode</strong> to <em>develop</em> and the <strong>loadmode</strong> to <em>UART</em>.
  </li>
  <li>
    The next image shows the software environment that must be configured according to each release.
    <br>
    <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/Software%20Settings/Slide3.png?raw=true" alt="ESPRESSIF Flash Download Tools - Software Environment" style="max-width:600px;">
  </li>
  <li>
    The latest release is currently available <a href="https://github.com/mohammad1388f/SafeSpark/releases/tag/2.0" target="_blank">here</a>.
  </li>
  <li>
    Once all settings are configured, connect the board, press the Start button, and wait until the flashing process completes.
  </li>
</ol>

<h3>Arduino IDE</h3>
<p>
  The Arduino IDE allows you to modify code and settings. It requires the installation of the necessary libraries and the ESP32 Board Package. The installation link is provided in the <em>Prerequisites &amp; Installation</em> section.
</p>
<p>Installation Steps:</p>
<ol>
  <li>
    Open the Arduino IDE and select the DOIT ESP32 DevKit V1 board.
  </li>
  <li>
    Review the software environment as shown below:
    <br>
    <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/Software%20Settings/Slide1.png?raw=true" alt="Arduino IDE Environment" style="max-width:600px;">
  </li>
  <li>
    Click on the "Upload" button to flash the code to the board.
  </li>
</ol>

<h2 id="usage-guide">Usage Guide</h2>
<p>
  Upon powering up the board, it automatically creates a WiFi access point with the default credentials:
  <strong>SSID:</strong> BOOM &nbsp;&nbsp; <strong>Password:</strong> 12345678.
</p>
<p>
  Connect to this access point and either use your router's management interface or open a web browser and navigate to <code>192.168.4.1</code> to access the management page. This page includes two main buttons: <strong>Settings</strong> and <strong>BOOM!</strong>.
</p>
<p>
  In the <strong>Settings</strong> menu, you will find three options:
</p>
<ol>
  <li>
    <strong>Countdown:</strong> Set the duration for the countdown timer.
  </li>
  <li>
    <strong>LED Delay:</strong> Specify the time (in seconds) before the countdown ends when the relay activates. This causes the Tengestan spring to heat up and the firework fuse to ignite, ensuring the fuse burns in sync with the countdown, audio, and visual effects.
  </li>
  <li>
    <strong>LED On Duration:</strong> Set the time the relay remains on, allowing the Tengestan spring to stay hot long enough without causing damage.
  </li>
</ol>
<p>
  After configuring these settings, click the <strong>Save</strong> button to store them in the EEPROM.
</p>
<p>
  <img src="https://github.com/mohammad1388f/SafeSpark/blob/2.0/Usage%20Guide/Slide1.png?raw=true" alt="Usage Guide - Settings" style="max-width:600px;">
</p>
<p>
  In its normal, inactive state, the device displays a continuous rainbow effect. Pressing the <strong>BOOM!</strong> button initiates the countdown along with synchronized audio and visual effects. An orange blinking light on the Neopixel ring, synced with the sound, indicates the time remaining until the explosion. If the beep interval is 1 second, it signifies that 10 seconds or more remain; if less than 10 seconds remain, the interval decreases progressively until it reaches as low as 30 milliseconds. At the moment of explosion and immediately afterward, the Neopixel ring turns red for 2 seconds, then green for 4 seconds to indicate safety, before reverting back to the rainbow effect.
</p>
<p>
  Example video: click <a href="https://example.com" target="_blank">here</a> to view.
</p>

<h2 id="video-tutorial">Video Tutorial</h2>
<p>Coming soon ...</p>

<h2 id="code">Code</h2>
<p>Coming soon ...</p>

<h2 id="contribution">Contribution</h2>
<p>
  You can submit pull requests, report issues, and discuss improvements in the Issues or Discussions sections. For special collaboration inquiries, please use the contact information provided below.
</p>

<h2 id="contact">Contact &amp; About the Developer</h2>
<p>
  <strong>Instagram:</strong>
  <a href="https://instagram.com/mohammadavrcode" target="_blank">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a5/Instagram_icon.png/900px-Instagram_icon.png" alt="Instagram Logo" style="height:20px; vertical-align: middle;">
    @mohammadavrcode
  </a>
</p>
<p>
  <strong>Telegram:</strong>
  <a href="https://t.me/mohammadavrcode_en/2" target="_blank">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Telegram_logo.svg/768px-Telegram_logo.svg.png" alt="Telegram Logo" style="height:20px; vertical-align: middle;">
    @mohammadavrcode_en
  </a>
</p>
<p>
  <strong>Twitter (X):</strong>
  <a href="https://x.com/mohammadavrcode" target="_blank">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Logo_of_Twitter.svg/180px-Logo_of_Twitter.svg.png" alt="Twitter Logo" style="height:20px; vertical-align: middle;">
    @mohammadavrcode
  </a>
</p>

<h2 id="license">License</h2>
<p>
  This project is licensed under GPL 3.0. This license ensures that the software remains free and open-source, and that any modifications or redistributions are released under the same terms.
</p>

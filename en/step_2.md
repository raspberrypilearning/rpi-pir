## Detect motion with a PIR

![A digital illustration of a PIR (Passive Infrared) sensor module. The sensor has a white, dome-shaped cover on top of a green circuit board. The circuit board includes several electronic components and pins for connecting to other hardware.](images/pir_module.png)

### Wiring a PIR sensor

The pulse emitted when a PIR detects motion needs to be amplified, and so it needs to be powered. There are three pins on the PIR: they should be labelled **Vcc**, **Gnd**, and **Out**. These labels are sometimes concealed beneath the Fresnel lens (the white cap), which you can temporarily remove to see the pin labels.

![A digital illustration of a Raspberry Pi board connected to a PIR (Passive Infrared) sensor module. The Raspberry Pi, depicted in green, features various ports and a GPIO (General Purpose Input/Output) header. Three wires (blue, red, and black) connect the GPIO pins on the Raspberry Pi to the corresponding pins on the PIR sensor, which is shown to the right of the board with its white, dome-shaped cover.](images/pir_wiring.png)

--- task ---

Connect the **Vcc** pin needs to a **5V** pin on the Raspberry Pi.

--- /task ---

--- task ---

Connect the **Gnd** pin on the PIR sensor to **any** ground pin on the Raspberry Pi.

--- /task ---

--- task ---

Lastly, the **Out** pin needs to be connected to **any** of the GPIO pins.

--- /task ---


### Tuning a PIR

Most PIR sensors have two potentiometers on them. These can control the sensitivity of the sensors, and also the period of time for which the PIR will signal when motion is detected.

![A close-up photograph of a PIR (Passive Infrared) sensor module viewed from the side. The image shows the white, dome-shaped sensor cover on top, with various electronic components, including capacitors and two orange potentiometers, visible beneath it on the green circuit board. The background is plain and white.](images/pir_pots.jpg)

In the image above, the potentiometer on the right controls the sensitivity, and the potentiometer on the left controls the timeout. Here, both are turned fully anti-clockwise, meaning that the sensitivity and timeout are at their lowest.

When the timeout is turned fully anti-clockwise, the PIR will output a signal for about 2.5 seconds, whenever motion is detected. If the potentiometer is turned fully clockwise, the output signal will last for around 250 seconds. When tuning the sensitivity, it is best to have the timeout set as low as possible.

### Detecting motion

You can detect motion with the PIR using the code below:

```python
from gpiozero import MotionSensor

pir = MotionSensor(4)

while True:
	pir.wait_for_motion()
	print("You moved")
	pir.wait_for_no_motion()
```

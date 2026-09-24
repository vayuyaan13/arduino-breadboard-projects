# Arduino Breadboard Projects and Basics

A solderless breadboard lets you build and change low-voltage circuits without soldering. It is useful for Arduino sensors, LEDs, buttons, and beginner electronics projects.

## What is a breadboard?

A breadboard contains groups of electrically connected holes. Components placed in the same connected group share an electrical node.

Most full-size boards have a central gap separating the two terminal areas. Power rails are often provided along the sides.

For a beginner explanation of breadboard construction, connections, and practical use, see this [bread board](https://vayuyaan.com/blog/what-is-bread-board/) guide.

## Power rails

Power rails marked + and - can distribute 5V and GND around a circuit.

Do not assume that a rail is continuous from one end to the other. Some boards split rails in the middle. Check the board layout or use a multimeter.

## Arduino Uno wiring

A common setup is:

- Arduino GND → breadboard ground rail
- Arduino 5V → positive rail when appropriate
- Components → terminal strips
- Arduino I/O pins → circuit nodes through jumper wires

Avoid putting both legs of a component into the same connected row because that can bypass the component.

## LED test circuit

Connect:

Arduino pin 8 → 220–330 Ω resistor → LED anode

LED cathode → GND

~~~cpp
const int LED_PIN = 8;

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_PIN, HIGH);
  delay(1000);
  digitalWrite(LED_PIN, LOW);
  delay(1000);
}
~~~

Always use a current-limiting resistor with a basic LED circuit.

## Push-button input

A button can connect a digital pin to GND while using the Arduino's internal pull-up:

~~~cpp
const int BUTTON_PIN = 2;
const int LED_PIN = 8;

void setup() {
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  bool pressed = digitalRead(BUTTON_PIN) == LOW;
  digitalWrite(LED_PIN, pressed ? HIGH : LOW);
}
~~~

With INPUT_PULLUP, an open button reads HIGH and a pressed button reads LOW.

## Common mistakes

**Nothing works:** check GND first, then verify each connection.

**LED does not light:** check LED polarity and resistor placement.

**Sensor readings are wrong:** verify VCC, GND, signal pin, and Arduino pin numbers.

**Circuit works until wires move:** inspect loose jumper wires and worn breadboard contacts.

**Unexpected short circuit:** trace the electrical path rather than relying on physical proximity.

## Multimeter checks

With power removed:

1. Select continuity mode.
2. Check which holes are electrically connected.
3. Verify ground paths.
4. Check for shorts between power and ground.

Do not use continuity mode on a powered circuit unless your meter specifically allows it.

## Breadboard limitations

Breadboards are excellent for prototypes but are not suitable for every application.

Avoid using them for:

- Mains voltage
- High-current motors
- High-power heaters
- Permanent installations
- Circuits requiring very low electrical noise

Motors and switching circuits can create electrical noise and unreliable connections. Move a finished design to suitable wiring or a PCB when required.

## Good prototyping habits

- Keep wires organized.
- Use a consistent ground.
- Document important Arduino pins.
- Test one section at a time.
- Use external supplies for high-current loads.
- Disconnect power before changing wiring.
- Photograph a working prototype before dismantling it.

## Beginner projects

Try:

1. LED blink
2. Push-button counter
3. LDR light detector
4. Ultrasonic distance indicator
5. Temperature sensor display
6. Servo control
7. Buzzer alarm

## When to move to a PCB

Use a soldered prototype or PCB when the circuit must survive movement, carry higher current, reduce noise, or become a permanent installation.

## License

This project is provided under the repository license.

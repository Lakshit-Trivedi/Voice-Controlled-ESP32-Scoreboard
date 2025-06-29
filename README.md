# Voice-Controlled-ESP32-Scoreboard
ClapToScore is a voice-controlled digital scoreboard built using an ESP32, a KY-038 sound sensor, and a TM1637 4-digit 7-segment display. It uses simple clap patterns to control the scoreboard without needing any buttons or remotes.

- 👏 *One clap* → Adds 1 point to *Team A*
- 👏👏 *Two claps* → Adds 1 point to *Team B*
- 🔄 Press the reset button to reset the scores



## 🔧 Hardware Components

| Component              | Quantity |
|------------------------|----------|
| ESP32 Dev Board        | 1        |
| KY-038 Sound Sensor    | 1        |
| TM1637 4-Digit Display | 1        |
| Push Button            | 1        |
| Jumper Wires           | ~        |
| Breadboard             | 1        |

---

## 🔌 Circuit Connections

| Module        | ESP32 Pin |
|---------------|-----------|
| KY-038 (A0)   | GPIO 34   |
| TM1637 CLK    | GPIO 22   |
| TM1637 DIO    | GPIO 21   |
| Reset Button  | GPIO 15 (to GND) |

📝 *Note: KY-038 works better using the **digital output* for clap detection in this setup.

---

## 💡 Features

- Hands-free scoreboard update using *claps*
- Compact and low-cost hardware setup
- Live score display on 7-segment display
- Easy reset using push button
- Serial output for debugging or serial monitoring

---

## 📜 Code Overview

### 📌 Clap Detection Logic
- The code detects *rising edges* (LOW → HIGH transitions) from the KY-038 digital pin.
- When a *clap is detected*, the code timestamps the first clap.
- If a *second clap* follows within maxClapGap (500 ms), it's counted as a *double clap* (Team B scores).
- If no second clap arrives in time, it's a *single clap* (Team A scores).

### 🔁 Main Variables

| Variable            | Purpose                                       |
|---------------------|-----------------------------------------------|
| clapCount         | Number of claps detected                      |
| firstClapTime     | Timestamp of the first clap                   |
| maxClapGap        | Max time between 2 claps (for double clap)    |
| teamAScore/teamBScore | Score counters                        |

---

## 🔢 Display Format

The TM1637 4-digit display shows scores in AA:BB format where:

- AA → Team A's score
- BB → Team B's score
- Colon (:) is used to separate the two

Example: 05:03 means Team A has 5 points and Team B has 3.

---

## 🛠️ How to Use

1. Connect all components as shown.
2. Upload the code to the ESP32 using Arduino IDE.
3. Open the Serial Monitor at 115200 baud for logs.
4. Clap:
   - Once → Team A gets a point.
   - Twice quickly → Team B gets a point.
5. Press the reset button to reset both scores to 00:00.

---

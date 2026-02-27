Arduino-Based Automatic Toll Gate System
📌 Project Description

- This project is an Arduino-Based Automatic Toll Gate System that uses RFID technology to automatically open and close a toll gate. When an authorized RFID card is scanned, the system verifies the card and activates a servo motor to lift the gate. Unauthorized cards will not open the gate.

- The purpose of this project is to demonstrate how automation can improve traffic flow and reduce manual toll operations.

🛠Components Used
1. Arduino Uno
2. RFID Module 
3. RFID Card/Tag
4. Servo Motor
5. Ultrasonic Sensor (for future implementation)
6. Breadboard
7. Jumper Wires
8. Power Supply

⚙ How It Works
- The system waits for an RFID card to be scanned.
- When a card is detected, the system checks if the UID is authorized.
- If authorized, the servo motor rotates to open the gate.
- And, the LCD display shows
- After a few seconds, the servo returns to its original position to close the gate.
- If the card is not authorized, the gate remains closed.

💻 How to Run the Project
- Connect all components according to the circuit diagram.
- Install required Arduino libraries
- Open Automatic_Tollgate.ino in Arduino IDE.
- Upload the code to the Arduino Uno.
- Power the board and test using an RFID card.

📷 Project Files Included
- Automatic_Tollgate.ino – Main project code
- Group4_Arduino_Automatic_Tollgate.pdf – Project documentation
- Project photos
- README.md

🚧 Current Status
The RFID, servo motor system, and LCD display is fully implemented and tested. Minor code adjustments were made to fix small errors. The diorama model is currently under construction. An ultrasonic sensor will be added in the next phase.

🔮 Future Improvements
- Add ultrasonic sensor for vehicle detection
- Improve diorama structure
- Enhance system security

👥 Group Members
Kith Bryan F. Asuncion
Jade Ann Ucab
Alona G. Abar
Janilla B. Cabana 
Denmark Y. Pamisa
Kim Edmond T. Valdehueza 

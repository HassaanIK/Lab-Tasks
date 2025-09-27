# PF Assignment 2

--- 

## Problem 1

### Task

You are given an amount of money. The program should calculate how many notes of each denomination (2000, 500, 200, …, 1) are needed to make that amount.

### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    int amount;
    int count;

    cout << "Enter the amount: ";
    cin >> amount;

    cout << "Currency Note : Number\n";

    // 2000 notes
    count = amount / 2000;
    amount = amount % 2000;
    cout << "2000 : " << count << endl;

    // 500 notes
    count = amount / 500;
    amount = amount % 500;
    cout << "500  : " << count << endl;

    // 200 notes
    count = amount / 200;
    amount = amount % 200;
    cout << "200  : " << count << endl;

    // 100 notes
    count = amount / 100;
    amount = amount % 100;
    cout << "100  : " << count << endl;

    // 50 notes
    count = amount / 50;
    amount = amount % 50;
    cout << "50   : " << count << endl;

    // 20 notes
    count = amount / 20;
    amount = amount % 20;
    cout << "20   : " << count << endl;

    // 10 notes
    count = amount / 10;
    amount = amount % 10;
    cout << "10   : " << count << endl;

    // 1 notes
    count = amount / 1;
    amount = amount % 1;
    cout << "1    : " << count << endl;

    return 0;
}
```

### Explanation

Division (`/`) → finds how many notes fit into the current amount.

Modulus (`%`) → finds the remaining amount after using those notes.

Step-by-step deduction → biggest note first, then smaller notes.




## Problem 2

### Task

You’re writing a program for a retail company that generates a monthly sales tax report.

- Input: month, year, total collected amount (sales + tax).

- Output: Sales, County Tax, State Tax, and Total Tax.

### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    string month;
    int year;
    double totalCollected, sales, stateTax, countyTax, totalTax;

    // Input values
    cout << "Enter month: ";
    cin >> month;
    cout << "Enter year: ";
    cin >> year;
    cout << "Enter total amount collected (including tax): ";
    cin >> totalCollected;

    // Tax rates
    double stateRate = 0.05;   // 5%
    double countyRate = 0.02;  // 2%
    double totalRate = stateRate + countyRate; // 7%

    // Calculate product sales (without tax) using formula
    sales = totalCollected / (1 + totalRate);

    // Calculate individual taxes
    stateTax = sales * stateRate;
    countyTax = sales * countyRate;
    totalTax = stateTax + countyTax;

    // Display report
    cout << "\nMonth: " << month << " " << year << endl;
    cout << "-------------------------------------------" << endl;
    cout << "Total Collected   : Rs. " << totalCollected << endl;
    cout << "Sales             : Rs. " << sales << endl;
    cout << "County Sales Tax  : Rs. " << countyTax << endl;
    cout << "State Sales Tax   : Rs. " << stateTax << endl;
    cout << "Total Sales Tax   : Rs. " << totalTax << endl;

    return 0;
}
```

### Explanation

- Division to remove tax → Formula: `Sales = Total Collected / (1 + TotalRate)`
- This removes the 7% tax from the total.
- Once you have Sales, you can multiply by tax rates to get state tax and county tax.
- Finally, add them for total tax.



## Problem 3

### Task 3 

A cyber café charges customers Rs. 50 per hour of internet usage.
You need to:

1. Take total minutes as input.

2. Convert into hours and remaining minutes.

3. Calculate total bill.

4. Display everything in a neat format.


### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    int minutes;
    cout << "Enter total minutes used: ";
    cin >> minutes;

    // Calculate hours and remaining minutes
    int hours = minutes / 60;
    int remaining = minutes % 60;

    // Bill for hours
    double bill = hours * 50;

    // Add charges for remaining minutes
    bill += (remaining / 60.0) * 50;

    // Display result
    cout << "\n--- Customer Bill ---\n";
    cout << "Hours used     : " << hours << endl;
    cout << "Minutes used   : " << remaining << endl;
    cout << "Total Bill (Rs): " << bill << endl;

    return 0;
}
```

### Explanation

Example: if the user enters 135 minutes

- `hours = 135 / 60 = 2`

- `remaining = 135 % 60 = 15`

So the usage is 2 hours and 15 minutes.

Remaining minutes are converted into fraction of an hour by dividing by 60.

`15 minutes = 15 / 60 = 0.25 hours`.

`Cost = 0.25 * 50 = Rs. 12.5`.

This makes the calculation fair (proportional billing).



## Problem 4

### Task

You need to simulate a checksum:

1. Take a 4-digit number as input.

2. Break it into individual digits.

3. Add all digits.

4. If the sum is divisible by 10 → Checksum valid ✅   Otherwise → Checksum invalid ❌

This mimics how real networking checks data integrity.

### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    int num, d1, d2, d3, d4, sum;
    cout << "Enter a 4-digit number: ";
    cin >> num;

    // Extract digits
    d1 = num % 10;   
    num /= 10;

    d2 = num % 10;   
    num /= 10;

    d3 = num % 10;   
    num /= 10;
    
    d4 = num % 10;

    // Add digits
    sum = d1 + d2 + d3 + d4;

    // Check checksum
    if (sum % 10 == 0)
        cout << "Checksum is valid" << endl;
    else
        cout << "Checksum is invalid" << endl;

    return 0;
}
```

### Explanation

This breaks the number into digits by repeatedly using:

`% 10` → last digit

`/= 10` → remove last digit

For 1234:

```
d1 = 1234 % 10 = 4

d2 = 123 % 10 = 3

d3 = 12 % 10 = 2

d4 = 1 % 10 = 1
```

So digits are: 1, 2, 3, 4.

Sum = 4 + 3 + 2 + 1 = 10.

If sum is divisible by 10, it’s valid, otherwise invalid.


## Problem 5

### Task

Write a program to simulate simple data security mechanisms like masking and obfuscation on a 4-digit PIN. 

Use XOR operation for masking and bit shifting for obfuscation, then recover the original data.

### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    int pin;
    int secretKey = 12;   // secret key for XOR

    cout << "Enter a 4-digit PIN: ";
    cin >> pin;

    // Masking with XOR
    int masked = pin ^ secretKey;

    // Obfuscation by shifting left
    int obfuscated = masked << 2;

    // Recover original: shift back then XOR again
    int recovered = (obfuscated >> 2) ^ secretKey;

    // Output results
    cout << "\n--- Data Security Simulation ---\n";
    cout << "Original Data   : " << pin << endl;
    cout << "Masked Data     : " << masked << endl;
    cout << "Obfuscated Data : " << obfuscated << endl;
    cout << "Recovered Data  : " << recovered << endl;

    return 0;
}
```

### Explanation

1. XOR Masking (`pin ^ secretKey`)

- XOR with a secret key scrambles the original data.

- Example: If `pin = 1234` and `secretKey = 12`, the masked result will be a new number.

2. Obfuscation (Shift Left)

- Shifting bits left (`<< 2`) increases security by adding another transformation step.

3. Recovery Process

- Reverse the shift (`>> 2`).

4. Apply XOR with the same key again to restore the original PIN.

Result

- `Original → Masked → Obfuscated → Recovered`

- Final recovered value matches the original, proving the method works.


## Problem 6

### Task

Simulate a permission control system using an 8-bit integer mask (0–255) where each bit represents a specific permission.

1. Display currently granted permissions.

2. Toggle (flip) the "Write file" permission.

3. Check if "Manage Users" permission is enabled.

4. Revoke (remove) the "Delete file" permission.


### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    int mask;   // 8-bit integer (0–255)
    cout << "Enter permission mask (0–255): ";
    cin >> mask;

    // Permission names (bit 0 → bit 7)
    string permissions[8] = {
        "Read file",          // bit 0
        "Write file",         // bit 1
        "Execute file",       // bit 2
        "Delete file",        // bit 3
        "Modify settings",    // bit 4
        "Access Logs",        // bit 5
        "Manage Users",       // bit 6
        "Admin Privileges"    // bit 7
    };

    // Step 1: Display granted permissions ~Checking which permissions are ON.
    cout << "\nPermissions granted:\n";
    for (int i = 0; i < 8; i++) {
        if (mask & (1 << i)) {   // check if bit i is set
            cout << "✔ " << permissions[i] << endl;
        }
    }

    // Step 2: Toggle "Write file" permission (bit 1 - Flipping a specific permission.
    mask = mask ^ (1 << 1);   // XOR flips bit 1 (ON->OFF or OFF->ON)
    cout << "\nAfter toggling 'Write file': " << mask << endl;

    // Step 3: Check if "Manage Users" permission (bit 6) is granted-Checking one permission.
    if (mask & (1 << 6))      // AND with (1<<6) checks if bit 6 is set
        cout << "Manage Users permission is granted.\n";
    else
        cout << "Manage Users permission is not granted.\n";

    // Step 4: Revoke "Delete file" permission (bit 3) - Removing one permission.
    mask = mask & ~(1 << 3);  // AND with NOT ensures bit 3 is 0
    cout << "After revoking 'Delete file': " << mask << endl;

    return 0;
}
```

### Explanation

1. Permission Mask (0–255):

- An integer between 0–255 represents 8 bits.

- Each bit corresponds to one permission (ON = granted, OFF = not granted).

2. Checking Permissions:

- (`mask & (1 << i)`) checks if bit i is ON.

- Example: if mask = 13 → binary 00001101, then Read, Write, and Delete are ON.

3. Toggling Permissions:

- `mask ^ (1 << 1)` flips bit 1 (Write permission).

- If it was ON → turns OFF, if OFF → turns ON.

4. Checking Specific Permission:

- `(mask & (1 << 6))` checks if "Manage Users" is granted.

5. Revoking Permission:

- `mask & ~(1 << 3)` forces bit 3 (Delete) to 0 → permission removed.


## Problem 7

### Task

A secret agency encodes each agent’s identity into a 32-bit integer. The number packs different pieces of information in specific bit ranges:

- Bits 31–24 (8 bits): Clearance Code

- Bits 23–18 (6 bits): Mission Batch No.

- Bits 17–6 (12 bits): Operation Log No.

- Bits 5–0 (6 bits): Unit Assignment No.

Write a program that extracts these fields from the encoded identity using bitwise operators and displays the information alongside the agent’s name.

### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    unsigned int identity;   // 32-bit encoded identity
    char name[50];           // array for agent name

    // Input
    cout << "Enter 32-bit encoded agent identity (integer): ";
    cin >> identity;
    cout << "Enter Secret Agent Name: ";
    cin >> name;   // simple input for name

    // Extract values using bitwise operators
    int clearanceCode = (identity >> 24) & 255;   // 8 bits mask = 255 (11111111)
    int missionBatch  = (identity >> 18) & 63;    // 6 bits mask = 63 (111111)
    int operationLog  = (identity >> 6)  & 4095;  // 12 bits mask = 4095 (111111111111)
    int unitAssign    = identity & 63;            // last 6 bits mask = 63

    // Output
    cout << "\n--- Secret Agent Info ---\n";
    cout << "Agent Name          : " << name << endl;
    cout << "Clearance Code      : " << clearanceCode << endl;
    cout << "Mission Batch No.   : " << missionBatch << endl;
    cout << "Operation Log No.   : " << operationLog << endl;
    cout << "Unit Assignment No. : " << unitAssign << endl;

    return 0;
}
```

### Explanation

1. Bit Shifting & Masking

- `>>` shifts bits to the right, moving the required part into the least significant bits.

- `&` (bitwise AND) with a mask isolates only the required bits.

2. Field Extraction

- Clearance Code: `(identity >> 24) & 255`

  -  Shifts top 8 bits down, masks with `11111111`.

- Mission Batch: `(identity >> 18) & 63`

  -  Shifts 6 bits down, masks with `111111`.

- Operation Log: `(identity >> 6) & 4095`

  -  Shifts 12 bits down, masks with `111111111111`.

- Unit Assignment: `identity & 63`

  -  Directly masks last 6 bits.

4. Input/Output

- User enters a 32-bit encoded integer and agent’s name.

- Program decodes and prints all details neatly.


## Problem 8

### Task

You are given a 32-bit packet header (in hexadecimal format). The program should:

1. Extract the Packet Type (top 4 bits).

2. Extract the Destination Port (next 12 bits after shifting right by 16).

3. Flag the packet as suspicious if:

  -  Packet Type = 15, or

  -  Destination Port < 1024

### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    unsigned int header;

    // Input packet header in hex
    cout << "Enter packet header (in hex, e.g., 0x81F345A2): ";
    cin >> hex >> header;   // read in hexadecimal format

    // Extract Packet Type (top 4 bits)
    int packetType = header >> 28;    // move top 4 bits down

    // Extract Destination Port (next 12 bits after shifting right by 16)
    int destinationPort = (header >> 16) & 0xFFF; // keep only 12 bits

    // Output extracted values
    cout << "\nPacket Type: " << packetType << endl;
    cout << "Destination Port: " << destinationPort << endl;

    // Check for suspicious conditions
    if (packetType == 15 || destinationPort < 1024) {
        cout << "Suspicious packet flagged for review.\n";
    } else {
        cout << "Packet looks normal.\n";
    }

    return 0;
}
```

### Explanation

- `cin >> hex >> header;` → Reads the input in hexadecimal format (e.g., 0x81F345A2).

- `packetType = header >> 28;` → Shifts the top 4 bits down to extract the Packet Type.

- `destinationPort = (header >> 16) & 0xFFF;` → Shifts right by 16 bits and applies a mask (`0xFFF`) to extract 12 bits for the port.

- Suspicious check:

  -  Packet Type = 15 → highest possible type → unusual.

  -  Destination Port < 1024 → reserved ports, hence suspicious.

This simulates how network firewalls or IDS systems analyze headers for anomalies.


## Problem 9

### Task

This program simulates a SafeBank Security System with multiple security-related functionalities.
The user chooses from a menu (1–8), and the program performs the selected task:

1. **Message Encryption with ASCII Shift** → Encrypts and decrypts a character using a simple shift.

2. **Secure Salary Calculation** → Calculates final salary after bonus, allowance, and tax.

3. **Data Transmission with Rotation** → Rotates an 8-bit value left and right, then XORs results.

4. **XOR-based Encryption** → Encrypts and decrypts a character using three XOR keys.

5. **Security Bit Check** → Checks and toggles specific bits in an 8-bit number.

6. **Parity Check** → Counts set bits, determines parity, and inverts bits.

7. **Multiplication Using Shifts** → Multiplies a number by shifting and adding.

8. **Modular Arithmetic** → Applies modular operation for secure wrapping of values.


### Code

```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;
    cout << "=== SafeBank Security System ===" << endl;
    cout << "1. Message Encryption with ASCII Shift" << endl;
    cout << "2. Secure Salary Calculation" << endl;
    cout << "3. Data Transmission with Rotation" << endl;
    cout << "4. XOR-based Encryption" << endl;
    cout << "5. Security Bit Check" << endl;
    cout << "6. Parity Check" << endl;
    cout << "7. Multiplication Using Shifts" << endl;
    cout << "8. Modular Arithmetic" << endl;
    cout << "Enter your choice (1-8): ";
    cin >> choice;

    if (choice == 1) {
        char ch;
        cout << "Enter a character to encrypt: ";
        cin >> ch;
        char encrypted = (ch + 5) % 128;
        char decrypted = (encrypted - 5 + 128) % 128;
        cout << "Encrypted character: " << encrypted << endl;
        cout << "Decrypted character: " << decrypted << endl;
    }
    else if (choice == 2) {
        double salary;
        cout << "Enter the basic salary: ";
        cin >> salary;
        double finalSalary = ((salary * 1.5) + 500) * 0.9;
        cout << "Final salary after tax: " << finalSalary << endl;
    }
    else if (choice == 3) {
        unsigned char val;
        cout << "Enter an 8-bit value (0-255): ";
        cin >> val;
        unsigned char leftRot = ((val << 3) | (val >> (8 - 3))) & 0xFF;
        unsigned char rightRot = ((val >> 3) | (val << (8 - 3))) & 0xFF;
        unsigned char result = leftRot ^ rightRot;
        cout << "Result after combining rotations: " << (int)result << endl;
    }
    else if (choice == 4) {
        char ch;
        int k1, k2, k3;
        cout << "Enter a character: ";
        cin >> ch;
        cout << "Enter 3 keys: ";
        cin >> k1 >> k2 >> k3;
        char encrypted = ch ^ k1 ^ k2 ^ k3;
        char decrypted = encrypted ^ k1 ^ k2 ^ k3;
        cout << "Encrypted character: " << encrypted << endl;
        cout << "Decrypted character: " << decrypted << endl;
    }
    else if (choice == 5) {
        unsigned char val;
        cout << "Enter an 8-bit value: ";
        cin >> val;
        int bit2 = (val >> 1) & 1;
        int bit5 = (val >> 4) & 1;
        cout << "2nd bit is " << bit2 << endl;
        cout << "5th bit is " << bit5 << endl;
        val = val ^ (1 << 5);
        cout << "Value, after toggling the 6th bit: " << (int)val << endl;
    }
    else if (choice == 6) {
        unsigned char val;
        cout << "Enter an 8-bit value: ";
        cin >> val;
        int count = 0;
        unsigned char temp = val;
        for (int i = 0; i < 8; i++) {
            count += temp & 1;
            temp >>= 1;
        }
        int parity = count % 2; // 0 = odd, 1 = even
        unsigned char inverted = ~val & 0xFF;
        cout << "Parity = " << parity << endl;
        cout << "Inverted value: " << (int)inverted << endl;
    }
    else if (choice == 7) {
        int num;
        cout << "Enter a number: ";
        cin >> num;
        int result = (num << 4) + 250;
        cout << "Final Result : " << result << endl;
    }
    else if (choice == 8) {
        int num;
        cout << "Enter a number: ";
        cin >> num;
        int result = ((num % 256) + 100) % 256;
        cout << "Final result: " << result << endl;
    }
    else {
        cout << "Invalid choice!" << endl;
    }

    return 0;
}
```

### Explanation

#### 1. **Option 1 – Message Encryption with ASCII Shift**

- Encryption: encrypted = (ch + 5) % 128

  -  Adds 5 to ASCII value of character.

  -  % 128 ensures it stays in ASCII range (0–127).

- Decryption: decrypted = (encrypted - 5 + 128) % 128

  -  Subtracts 5.

  -  +128 prevents negative numbers before % 128.

- Example:
  -  Input 'A' (65) → 65+5=70 → 'F'.
  -  Decrypt: 70-5=65 → 'A'.
 

#### 2. **Option 2 – Secure Salary Calculation**

Formula: `finalSalary = ((salary * 1.5) + 500) * 0.9`

Steps:

1. `salary * 1.5` → adds 50% bonus.

2. `+ 500` → adds allowance.

3. `* 0.9` → applies 10% tax deduction.

- Example:
Input salary = `10000`

- Bonus = `10000 * 1.5 = 15000`

- +Allowance = `15000 + 500 = 15500`

- Tax = `15500 * 0.9 = 13950.`

#### 3. **Option 3 – Data Transmission with Rotation**

Left Rotation by 3:
- `(val << 3) | (val >> (8-3))` → shifts left 3 bits, moves overflowed bits to right.

Right Rotation by 3:
- `(val >> 3) | (val << (8-3))` → shifts right 3 bits, moves overflowed bits to left.

Final Result: `leftRot ^ rightRot` → XOR combines both rotations.

✅ Example:
Input = `10110011` (179)

Left Rot(3) = `10011101` (157)

Right Rot(3) = `01110110 `(118)

XOR = `11101011` (235).

#### 4. **Option 4 – XOR-based Encryption**

- Encryption: `encrypted = ch ^ k1 ^ k2 ^ k3`

- Decryption: `decrypted = encrypted ^ k1 ^ k2 ^ k3`

Property: XOR is self-inverse, so applying same keys again recovers original.

✅ Example:

Input `'A'` (65), keys `3, 5, 7`:
- Encrypt: `65 ^ 3 ^ 5 ^ 7 = 66 ('B')`.

- Decrypt: `66 ^ 3 ^ 5 ^ 7 = 65 ('A')`.

#### 5. **Option 5 – Security Bit Check**

- bit2 = `(val >> 1) & 1 `→ extracts 2nd bit.

- bit5 = `(val >> 4) & 1` → extracts 5th bit.

- Toggle 6th bit: `val = val ^ (1 << 5)`

  - ` 1 << 5 = 00100000 `→ flips the 6th bit.

✅ Example:
Input = `00101101` (45)

- 2nd bit = `0`

- 5th bit = `1`

- Toggle 6th → `01101101` (109).

#### 6. **Option 6 – Parity Check**

- Count set bits (1s).

- `parity = count % 2`

  -  `0` → odd parity

  -  `1` → even parity

Invert: `~val & 0xFF` → flips all 8 bits.

✅ Example:
Input = `11010010` (210)

Count = 4 ones (even).

Parity = 1.

Invert = `00101101` (45).

#### 7. **Option 7 – Multiplication Using Shifts**

Formula: `result = (num << 4) + 250`

Steps:

- `num << 4` = multiply number by `2^4 = 16`.

Add 250 offset.

✅ Example:
Input `10`:

- `10 << 4 = 160`.

- +250 = 410.


#### 8. **Option 8 – Modular Arithmetic**

Formula: `result = ((num % 256) + 100) % 256`

Steps:

1. `num % 256` → reduces number to range 0–255.

2. `+100 `→ adds offset.

3. `% 256 `→ ensures result still within 0–255.

✅ Example:
Input 200:

Step 1: `200 % 256 = 200`.

Step 2: `200 + 100 = 300`.

Step 3: `300 % 256 = 44`.

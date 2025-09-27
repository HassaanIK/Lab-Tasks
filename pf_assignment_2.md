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

Bits 31–24 (8 bits): Clearance Code

Bits 23–18 (6 bits): Mission Batch No.

Bits 17–6 (12 bits): Operation Log No.

Bits 5–0 (6 bits): Unit Assignment No.

Write a program that extracts these fields from the encoded identity using bitwise operators and displays the information alongside the agent’s name.

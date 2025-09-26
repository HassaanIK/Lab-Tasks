# Lab Task 3

---

## Task 1: Reverse Number (Compound Operators)

### Problem
The user always enters a **5-digit number**. The task is to print the number in **reverse order**.  
We must use **compound operators** like `%` (modulus) and `/=` (division).

### Code
```cpp
#include <iostream>
using namespace std;

int main() {
    int num, rev;
    cout << "Enter 5 digit number: ";
    cin >> num;

    int d1 = num % 10;
    num /= 10;

    int d2 = num % 10;
    num /= 10;

    int d3 = num % 10;
    num /= 10;

    int d4 = num % 10;
    num /= 10;

    int d5 = num % 10;

    rev = d1 * 10000 + d2 * 1000 + d3 * 100 + d4 * 10 + d5;

    cout << "Reversed Number: " << rev;
    return 0;
}
```
### Explanation

- `% 10` extracts the last digit.
- `/= 10` removes the last digit.
- Each digit is then placed in reverse order by multiplying with powers of 10.

Example:
Input: `12345`

Digits: `5, 4, 3, 2, 1`

Reversed = `54321`



## Task 2: Part(a) The XOR Data Scrambler (^)

### Problem
XOR (^) can scramble and unscramble data. If we XOR a character with a key twice, we get the original value.

### Code
```cpp
#include <iostream>
using namespace std;

int main() {
    char a = 'B', scrambled, org;
    int key = 10;

    scrambled = a ^ key;
    org = scrambled ^ key;

    cout << "Original: " << a;
    cout << "\nScrambled: " << scrambled;
    cout << "\nUnscrambled: " << org;

    return 0;
}
```
### Explanation

`a ^ key` scrambles character.

`scrambled ^ key` brings it back.

Example:
Original = `B`

Scrambled = some new char (depends on XOR)

Unscrambled = `B`


## Task 3: Part (b) The Combination Lock (| and &)

### Problem: 

Each key has a unique code. Use bitwise operators to combine and check them.
`KEY_RED = 4
KEY_GREEN = 2
KEY_BLUE = 1`

### Code:

```cpp
#include <iostream>
using namespace std;

int main() {
    int blue = 1, green = 2, red = 4, masterKey, result;

    cout << "Combining both keys";

    masterKey = red | blue;
    cout << "\nMaster key is: " << masterKey;

    cout << "\nChecking for green key";
    result = masterKey & green;
    cout << "\nResult (0 means not present): " << result;

    return 0;
}
```

### Explanation:

`|` (OR) merges codes:` red | blue = 4 | 1 = 5`.

`&` (AND) checks if a key exists.

Example:
MasterKey = `5`

Checking GREEN: `5 & 2 = 0 → Not present`

## Task 3: Store Discount Calculator

### Problem: 
Calculate final bill after discount and tax.

### Code:
```cpp
#include <iostream>
using namespace std;

int main() {
    float orgPrice, quantity, origTotal, discPrice, tax, taxPercentage, discPercentage, afterDisc, finalAmount, totalSavings;

    cout << "Enter item price:";
    cin >> orgPrice;

    cout << "Enter item quantity:";
    cin >> quantity;

    cout << "Enter Discount Percentage:";
    cin >> discPercentage;

    cout << "Enter Tax Percentage:";
    cin >> taxPercentage;

    origTotal = orgPrice * quantity;
    cout << "\nOriginal Total: " << origTotal;

    discPrice = origTotal * (discPercentage / 100);
    cout << "\nDiscount Price: " << discPrice;

    afterDisc = origTotal - discPrice;
    cout << "\nAfter Discount Price: " << afterDisc;

    tax = afterDisc * (taxPercentage / 100);
    cout << "\nTotal Tax: " << tax;

    finalAmount = afterDisc + tax;
    cout << "\nFinal Total: " << finalAmount;

    totalSavings = origTotal - finalAmount;
    cout << "\nTotal Savings: " << totalSavings;

    return 0;
}
```

### Explanation:

origTotal = `price × quantity.`
Discount applied → `discPrice`.
Tax applied on discounted price.
Add tax → `finalAmount`.
Savings = `origTotal - finalAmount`.

## Task 4: Library Book Organizer

### Problem:
Each shelf holds `25 books`. Calculate:

Full shelves
Leftover books
Total shelves required

### Code: 

```cpp
#include <iostream>
using namespace std;

int main() {
    int inputBooks, booksPerShelf, fullShelves, booksLastShelve, totalShelvesReq;

    booksPerShelf = 25;

    cout << "Enter number of Books:";
    cin >> inputBooks;

    fullShelves = inputBooks / booksPerShelf;
    cout << "\nFull shelves needed: " << fullShelves;

    booksLastShelve = inputBooks % booksPerShelf;
    cout << "\nBooks on the last shelf: " << booksLastShelve;

    totalShelvesReq = fullShelves + (booksLastShelve > 0 ? 1 : 0);
    cout << "\nTotal Shelves Required: " << totalShelvesReq;

    return 0;
}
```
### Explanation

`/` finds full shelves.

`%` finds leftover books.

If leftovers exist, add 1 more shelf.


## Task 5: Ride-Sharing Fuel Cost

### Problem: 
Road trip = `600 km`, car mileage = `15 km/L`, petrol = `290 Rs/L`, 4 friends share cost.

### Code: 
```cpp
#include <iostream>
using namespace std;

int main() {
    float distance, fuelEfficiency, petrolReq, totalCost, costPerLitre, costPerPerson, numPeople;

    cout << "Enter Distance:";
    cin >> distance;

    cout << "Enter Fuel Efficiency:";
    cin >> fuelEfficiency;

    cout << "Enter number of people:";
    cin >> numPeople;

    cout << "Enter cost per litre:";
    cin >> costPerLitre;

    petrolReq = distance / fuelEfficiency;
    cout << "\nPetrol Required: " << petrolReq;

    totalCost = petrolReq * costPerLitre;
    cout << "\nTotal Cost: " << totalCost;

    costPerPerson = totalCost / numPeople;
    cout << "\nCost Per Person: " << costPerPerson;

    return 0;
}
```

### Explanation

Petrol required = `distance ÷ fuel efficiency`.

Multiply by cost per litre → `totalCost`.

Divide by number of people → `costPerPerson`.

Example:

Distance = 600, Mileage = 15 → 40L petrol.

40 `×` 290 = Rs. 11,600 total.

11,600 `÷` 4 = Rs. 2,900 per person.

#### This was the simplest document I could make!!🙃

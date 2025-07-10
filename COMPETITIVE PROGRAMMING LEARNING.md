# What I Learned from competitive programming

## 1. Lexicographical comparison->
    
> Lexicographical comparison হলো C++-এ স্ট্রিং (string) তুলনা করার একটি পদ্ধতি যা অভিধান অনুযায়ী (dictionary order) কাজ করে। C++ সরাসরি স্ট্রিংগুলিকে তুলনা করতে পারে <, >, == এই অপারেটর ব্যবহার করে। উদাহরণস্বরূপ, যদি আমরা "ab" < "cd" লিখি, তাহলে C++ প্রথম অক্ষর দুটি — 'a' এবং 'c' — এর মধ্যে তুলনা করে। এটি প্রতিটি অক্ষরের ASCII মান বের করে এবং তাদের তুলনা করে। যেহেতু 'a'-এর ASCII মান 'c'-এর চেয়ে ছোট, তাই C++ মনে করে "ab" ছোট "cd" এর চেয়ে। Problem -> Petya and Strings (800 rating) 112A [Implemation + string].

## 2. Conversion->

> If you want to convert A to a then just add 32 to A. for example: (A + 32).  
> If you want to convert a to A then just substract 32 from A. for example: (A - 32).  
> If you want to convert character '1', '2' and '3' to digit 1, 2 and 3 then substract '0' from all character types integer. For example: '3' - '0' = 3, ASCII => 51 - 48 = 3.


## 3. How to remove any symbol from the last iteration after number printing->

```c++
    if(i != arr.size() - 1) {
        cout << '+';
    }
```

## 4. Problem of Pow() function with Big integers->

> Loss of Precision (Floating Point Inaccuracy)  
   Integer Overflow - Overflow (If cast to Integer)  
   Modulo error - Cannot use pow() reliably with %  
   Slower Performance - pow() is less efficient than bit-based methods.  
   For example: `pow(5,2)` = 25 but the code will 24. This is the problem when there is type mismatch.  
   How can we fix it?  
   = It is simple, we use `round()` function for this problem. `round(pow(5,2))` this should solve the problem. Also, there is direct short cut solution if your doing only square or cube. Just do a * a for square and a * a * a for cube. It will avoid error.


## 5. What is two pointer?

> Two pointer is just two normal variable which we use as a indices. It is not an actual memory pointer(int*). One variable take the index of the first item of the array and another variable takes the index of the last item.

```cpp
bool twoPointerPairExists(int arr[], int n, int target) {
    int left = 0;
    int right = n - 1;

    while (left < right) {
        int sum = arr[left] + arr[right];

        if (sum == target) {
            cout << "Pair found: " << arr[left] << " + " << arr[right] << " = " << target << endl;
            return true;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    cout << "No pair found with the given sum." << endl;
    return false;
}
```

## 6. How to get last one, two or three digit's:
>a = x % 10` **->** For finding last value.  
  a = x % 100` **->** For finding last two value.  
  a = x % 1000` **->** For finding last three value.


## S. EK ->

> `getline(cin , line);` -> to take a line as input.

> `cin.ignore();` -> ignore new line from the buffer.

> `str.length()` / `length()` -> calculate length of a string.

> `arr.size()` / `size()` -> calculate length of a array.

> `stoi(a)` -> This method helps to convert string into integers. We can not typecast string unless it's a single character. `stol(a)` -> long ; `stof(a)` -> float ; `to_string(a)` -> int to string.

> `find(vector.begin(), vector.end(), 2)` -> find the value '2' from the start and to the end of the vector. If not found then it will return the 2nd parameter(vector.end() is the 2nd parameter here).

> Sorting algorithm in c++ for vector (using algorithm and vector library) -> sort(arr.begin(),arr.end());  
   here, arr.begin()-> vector's first value and arr.end()-> vector's last value. Problem -> Helpful Math (800 rating) 339A [math, sorting, greedy].
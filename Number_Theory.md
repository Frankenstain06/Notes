# <span style= "color:#00FF00">Number Theory</span>

### <span style = "color:#DDA0DD">Divisor and Multiple</span>:
>  5 is the divisor of 50 and 50 is the multiple of 5. Here remainder is zero which means, 50 is completely divisibled by 5.

### <span style = "color:#DDA0DD">Modulo</span>:
>Modulo operator = '%'  
	`a % b` = remainder is the answer.    
	`12 % 3 = 0` -> here the remainder is zero.  
    `11 % 3 = 2` -> here the remainder is two.


>In terms of (a < b) ->  
	`a % b = a` (a will always be the remainder if it is less than b).      
	`3 % 8 = 3` -> here the remainder is three.
	
>	In terms of 'a' is negative (-a % b) ->  
	Example: `-7 % 5`  
	Take absolute value: | -7 | = 7  
	Do: `7 % 5 = 2`  
	Now: `5 - 2 = 3`  
	✅ Answer: -7 % 5 = 3

> In terms of 'b' is negative `(a % -b)` ->
Example: `7 % -5`  
Just simply make the b positive: | -5 | = 5  
Do: `7 % 5 = 2`  
✅ Answer: 7 % -5 = 2


#### <span style = "color:#DDA0DD">Modulo Arithmetic Properties</span>:  
> 1. `(a + b) % m = (a % m + b % m) % m`.  - addition  
> 2. `(a - b) % m = (a % m - b % m + m) % m`.  - subtraction   
> 3. `(a × b) % m = (a % m × b % m) % m`.  - multipication  
> 4. `(a × inverse(b)) % m.`  - division


#### <span style = "color:#DDA0DD">Modular Inverse</span>:
>গাণিতিকভাবে কোনো সংখ্যার ইনভার্স বলতে বোঝায় এমন একটি সংখ্যা, যেটিকে মূল সংখ্যার সঙ্গে গুণ করলে ফলাফল হয় ১। যেমন, 5 × $\frac{1}{5}$ = 1, অর্থাৎ $\frac{1}{5}$ হচ্ছে ৫-এর ইনভার্স। একইভাবে, ইনভার্সকে $5⁻¹$ দিয়েও প্রকাশ করা যায়। তবে যখন এই গুণফলের ওপর একটি **মডুলো অপারেশন** প্রয়োগ করা হয়, তখন ইনভার্সের সংজ্ঞা পরিবর্তিত হয় এবং তাকে বলা হয় **মডুলার ইনভার্স**। মডুলার ইনভার্স বোঝার জন্য আমরা ধরি, `a × U ≡ 1 (mod m)`, যেখানে `a` হলো মূল সংখ্যা, `m` হলো মডুলো এবং `U` হচ্ছে সেই ইনভার্স, যাকে গুণ করলে `(a × U) % m = 1` হয়।  উদাহরণ: ধরি, `(5 × U) % 3 = 1`.   
  এখানে লক্ষ্য হচ্ছে এমন একটি সংখ্যা `U` খুঁজে বের করা, যেটি ৫-এর সঙ্গে গুণ করে ৩ দিয়ে ভাগ করলে ভাগশেষ ১ পাওয়া যায়।  
  আমরা কিছু মান দিয়ে চেষ্টা করলে দেখি:  1. `5 × 1 = 5`, `5 mod 3 = 2` ❌  2. `5 × 2 = 10`, `10 mod 3 = 1` ✅  
  সুতরাং, এখানে `U = 2`, অর্থাৎ `5⁻¹ mod 3 = 2`।




---

### <span style = "color:#DDA0DD">GCD - Greatest Common Divisor</span> [ <span style = "color: red">**Euclid’s Algorithm**</span> ] :
> Suppose 12 and 16 are two numbers. what are their divisor?  
   for 12 -> 1, 2, 3, 4, 6 and 12;  
   for 16 -> 1, 2, 4, 8 and 16;  
**What are the common divisor among these two?**  
   common divisor = 1, 2 and 4.  
 **what is the greatest one among these?**  
   GCD = 4.

#### <span style = "color:#DDA0DD">GCD Process</span>:
> 1. Suppose there are two numbers a and b. Before doing anything create a temporary variable called temp and set the value b in it.  
```cpp
 int temp = b;
 ```  
 > 2. Do the modulo a % b and set its value of (a%b) to b.   
 ```cpp
 b = a % b;
 ``` 
> 3. now assign the value of temp in a.  
```cpp
a = temp. Repeat until b == 0;
```

> 4. Repeat it untill b becomes zero.

#### <span style = "color:#DDA0DD">GCD Code</span>:
```cpp
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}
```

---

### <span style = "color:#DDA0DD">LCM-Least Common Multiple</span>:
> Suppose there are two numbers a and b. multiply both numbers `(a*b)`. Then divide the multiple with GCD of those two numbers and you will get LCM.

#### Code:
```cpp
int LCM(int a, int b){
    int lcm = (a*b)/GCD(a,b);

    return lcm;
}
```

---
### <span style = "color:#DDA0DD">Find the Prime (Code)</span>:
``` cpp
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}
```  
> What is the divisor of 16?  
-> 1, 2, 4, 8, 16;  
here,  
      1 x 16 = 16  
      2 x 8 = 16  
      4 x 4 = 16  
      **Same thing will happen in reverse way**  
      4 x 4 = 16  
      8 x 2 = 16  
      16 x 1 = 16  
We don’t need to check all the way up to the number itself or even half of it when checking if a number is prime. Why? Let’s say you’re checking if 16 is prime. You’ll notice that:  
2 × 8 = 16  
4 × 4 = 16  
8 × 2 = 16  
See what’s happening? Once you go past the square root (which is 4 in this case), you just start repeating the same pairs but in reverse. So if 8 × 2 is a factor, you already found 2 × 8 before. No need to check again.  
That’s why we only check up to the square root of the number. It saves time and avoids checking the same thing twice. Simple and efficient.  
This is why **`i * i <= n`** is used in the code.


#### <span style = "color:#DDA0DD">Sieve of Eratosthenes algorithm to find upto nth prime(Code)</span>:
```cpp
void sieve(int n) {
    vector<bool> is_prime(n+1, true);
    is_prime[0] = is_prime[1] = false;

    for (int i = 2; i * i <= n; i++) {
        if (is_prime[i]) {
            for (int j = i*i; j <= n; j += i)
                is_prime[j] = false;
        }
    }

    for (int i = 2; i <= n; i++) {
        if (is_prime[i]) cout << i << " ";
    }
}
```
---

### <span style = "color:#DDA0DD">Prime factorization code(Code)</span>:
```cpp
int n;
    cin >> n;
     for(int i = 2; i * i <= n; i++){
        while(n % i == 0){
            cout << i << ' ';
            n /= i;
        }
     }
     if(n > 1){
        cout << n << ' ';
     }
```

> প্রাইম ফ্যাক্টরাইজেশন (Prime Factorization) হল একটি সংখ্যাকে তার মৌলিক গুণনীয়কগুলোর (prime factors) গুণফল হিসেবে প্রকাশ করা।  
> 
> অর্থাৎ, একটি সংখ্যা কতগুলো মৌলিক সংখ্যার গুণফলে গঠিত, সেটাই আমরা বের করি।  
> 
> ✅ উদাহরণস্বরূপ:  
> 60 = 2 × 2 × 3 × 5 = 2² × 3 × 5  
> 
> এই ক্ষেত্রে 2, 3, 5 — সবগুলোই মৌলিক সংখ্যা (prime), এবং এদের গুণফল 60।  
> 
> 🔍 কিভাবে করি:
> 
> 1. ২ (প্রথম মৌলিক সংখ্যা) দিয়ে সংখ্যা ভাগ করা শুরু করি যতক্ষণ সম্ভব।  
> 2. এরপর ৩, ৫, ৭, ... এভাবে পরের পরের মৌলিক সংখ্যা দিয়ে ভাগ করি।  
> 3. যতক্ষণ না ভাগ শেষ হয়ে যায় বা সংখ্যা ১ হয়ে যায়, ততক্ষণ এভাবে চলতে থাকে।  
> 
> 🎯 লক্ষ্য:  
> প্রতিবার শুধু মৌলিক সংখ্যাগুলোকেই ভাগের জন্য ব্যবহার করতে হবে।  
> 
> 🕒 সময় জটিলতা (Efficient Method):  
> √n পর্যন্ত চেক করলেই যথেষ্ট কারণ n-এর বড় কোন ফ্যাক্টর থাকলে তার একটি ছোট ফ্যাক্টরও থাকবে।
> 
> 📌 প্রাইম ফ্যাক্টরাইজেশন সাধারণত গণিতে, এলগরিদম ডিজাইন, এনক্রিপশন, এবং প্রোগ্রামিং সমস্যার সমাধানে ব্যবহৃত হয়।

---
### 
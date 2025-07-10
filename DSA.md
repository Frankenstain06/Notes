# <span style = "color:00FF00">**DSA**</span>
---
## <span style="color:#FF0000">**Greedy Algorithm**</span>:
> এই সমস্যাটি একধরনের লোভী অ্যালগরিদম (Greedy Algorithm)-এর দৃষ্টান্ত। লোভী অ্যালগরিদম প্রতিটি ধাপে সর্বোত্তম (locally optimal) সিদ্ধান্ত গ্রহণ করে, এই আশায় যে এর ফলে গ্লোবাল অপ্টিমাম (সর্বোচ্চ বা সর্বনিম্ন সমাধান) পাওয়া যাবে। তবে এটি ভবিষ্যতের কোনো অবস্থা বিবেচনা করে না বা পূর্ববর্তী সিদ্ধান্তে ফিরে গিয়ে সংশোধনও করে না। উদাহরণস্বরূপ, ধরুন আপনি একটি সোনার খনিতে প্রবেশ করলেন। সামনে দুটি রাস্তা — একদিকে বামে, অন্যদিকে ডানে। আপনি দেখলেন বামদিকে ৩টি সোনা আছে, আর ডানদিকে কিছুই নেই। সুতরাং আপনি বামদিকটি বেছে নিলেন, কারণ এটিই সেই মুহূর্তে সর্বোত্তম সিদ্ধান্ত মনে হলো। কিন্তু আপনি একবার বামদিকে যাওয়ার পর আর ফিরে আসার সুযোগ নেই। আপনি সামনে এগিয়ে যান এবং দেখেন এরপর আর কোথাও সোনা নেই। অপরদিকে, আপনার বন্ধু যিনি প্রথমে ডানদিক বেছে নিয়েছিলেন, তিনি কিছুদূর যাওয়ার পর বিশাল পরিমাণ সোনা খুঁজে পেয়েছেন। এই পরিস্থিতি থেকে বোঝা যায়, লোভী কৌশল প্রতিটি ধাপে তাৎক্ষণিক লাভ দেখে সিদ্ধান্ত নেয় — কিন্তু পুরো সমাধান ক্ষেত্রটি (সমস্ত পথ বা সমস্ত বিকল্প) একবারে দেখে না বা ভবিষ্যৎ সম্ভাবনা বিবেচনা করে না। ফলে এটি সব সময় গ্লোবাল অপ্টিমাম সমাধান দেয় না।  
Conclusion:  
লোভী অ্যালগরিদম দ্রুত এবং সহজ সমাধান দিলেও এটি সব ক্ষেত্রে কার্যকর নয়। যখন ভবিষ্যতের অবস্থা বিবেচনা গুরুত্বপূর্ণ, তখন ডাইনামিক প্রোগ্রামিং বা ব্যাকট্র্যাকিং এর মতো কৌশল ব্যবহার করা ভালো।  

## <span style="color:#FF0000">**Time-Complexity**</span>:  
> Time complexity is a way to figure out how long a piece of code might take to run, especially as the input gets bigger. It helps us understand how efficient the code is. Basically, the faster it runs (especially with large inputs), the better the code is considered to be.  
`int arr = {40, 10, 25, 21, 5}` find 5 and 40 in this array.  
> Here, if you go through the array the machine will find 40 instantly so it will take constant time **(Best case)**. For 5, it will go through the whole array and going to find 5. So, it will take n(input size) time **(Worst case)**.  
> Sigma sign **->** Best case.  
> Big O sign **->** Worst case.  
> Thita sign **->** Average case.  

```cpp
for(int i = 0; i <= n; i++){
    for(int j = 0; j <= m; j++){
        a++;
    }
}
```
> **(n x m)** is the time complexity here.  

```cpp
for(int i = 0; i <= n; i++){
    a++;
}
for(int j = 0; j <= m; j++){
    a--;
}
```
> **(n + m)** is the time complexity here.  

## <span style="color:#FF0000">**Searching**</span>:

### <span style = "color:#DDA0DD">Binary search code</span>:

```cpp
int binarySearch(int arr[], int size, int target) {
    int low = 0;
    int high = size - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return -1;
}
```
> বাইনারি সার্চ একটি দক্ষ অনুসন্ধান (search) অ্যালগরিদম, যা **sorted array**-এর উপর কাজ করে।  
> 
> এতে আমরা প্রতিবার অ্যারেটিকে দুই ভাগে ভাগ করে খুঁজি, যাতে খোঁজার সময় কম লাগে।  
> 
> প্রথমে আমরা দুটি ইনডেক্স নেই — `low = 0` এবং `high = n - 1`।  
> এরপর আমরা একটি লুপ চালাই যতক্ষণ না `low` > `high` হয়।  
> 
> প্রতি ধাপে আমরা `mid` ইনডেক্স হিসেব করি:  
> `mid = (low + high) / 2` (বা integer division)।  
> 
> তারপর ৩টি কেস চেক করি:
> 
> 🔹 যদি `arr[mid] == target`, তাহলে আমরা খোঁজে পেয়েছি, এবং `mid` রিটার্ন করি।  
> 🔹 যদি `arr[mid] < target`, তাহলে target ডান পাশে আছে — তাই `low = mid + 1` করি।  
> 🔹 যদি `arr[mid] > target`, তাহলে target বাম পাশে আছে — তাই `high = mid - 1` করি।  
> 
> এভাবে আমরা প্রতি ধাপে খোঁজার পরিসর অর্ধেকে নামিয়ে আনি, এবং খোঁজার সময় হয় O(log n)।  
> 
> ❗ মনে রাখতে হবে, বাইনারি সার্চ শুধুমাত্র **sorted array**-এ কাজ করে। unsorted array-তে এটি ব্যবহার করা যাবে না।  
> The time complexity is O(log n);

## <span style="color:#FF0000">**Sort**</span>:

### <span style = "color:#DDA0DD">Selection Sort</span>:
```cpp
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;

        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex])
                minIndex = j;
        }

        swap(arr[i], arr[minIndex]);
    }
}
```
> এই সোর্টে আমরা একটি ভ্যারিয়েবল নেই `[minIndex]`, যা প্রতি ধাপে সবচেয়ে ছোট (minimum) মানের ইনডেক্স ধরে রাখবে।  
> 
> আমরা দুটি লুপ চালাবো — একটি বাইরের লুপ এবং একটি ভিতরের (নেস্টেড) লুপ।  
> 
> 🔹 বাইরের লুপটি চলবে `0` থেকে `n - 2` পর্যন্ত।  
> 🔹 ভিতরের লুপটি চলবে `i + 1` থেকে `n` পর্যন্ত।  
> 
> প্রতি ধাপে আমরা প্রথমেই `[minIndex]`-কে `i` হিসেবে সেট করি, অর্থাৎ বর্তমান ইনডেক্সকে ধরে নেই সবচেয়ে ছোট।  
> 
> এরপর ভিতরের লুপে `j` চলবে `i + 1` থেকে `n` পর্যন্ত। যদি `arr[j] < arr[minIndex]` হয়, তাহলে আমরা `minIndex`-কে `j` দিয়ে আপডেট করি।  
> 
> ভিতরের লুপ শেষ হওয়ার পর, `minIndex`-এ যে ইনডেক্স থাকে সেটিই সবচেয়ে ছোট মানের ইনডেক্স — তখন আমরা `arr[i]` এবং `arr[minIndex]`-কে একে অপরের সাথে swap করি।  
> 
> এভাবে প্রতি ধাপে ছোট মানগুলো বামে চলে আসে এবং অ্যারে ধীরে ধীরে sort হয়ে যায়।  


### <span style = "color:#DDA0DD">Bubble Sort</span>:
```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```
> বাবল সোর্ট (Bubble Sort) একটি সাধারণ এবং সহজবোধ্য সর্টিং অ্যালগরিদম, যা প্রতিবার পাশে পাশে থাকা উপাদানগুলো তুলনা করে এবং প্রয়োজনে তাদের অদল-বদল (swap) করে।  
> 
> এই অ্যালগরিদমে বড় উপাদানগুলো ধীরে ধীরে ডানের দিকে "বাবলের" মতো উঠে যায় — এজন্য এর নাম বাবল সোর্ট।  
> 
> আমরা দুটি nested loop চালাই:
> 
> 🔹 বাইরের লুপটি চলে `0` থেকে `n - 1` পর্যন্ত, যাতে সব উপাদান সঠিকভাবে সর্ট হয়।  
> 🔹 ভিতরের লুপটি চলে `0` থেকে `n - i - 1` পর্যন্ত, কারণ প্রতি ধাপে সবচেয়ে বড় উপাদান ডানে চলে যায়, তাই পরের ধাপে সেটি তুলনা করার দরকার হয় না।  
> 
> ভিতরের লুপে `arr[j]` এবং `arr[j+1]` তুলনা করা হয়:
> 
> 🔸 যদি `arr[j] > arr[j+1]`, তাহলে আমরা তাদের **swap** করি।  
> 
> এভাবে সবচেয়ে বড় উপাদান প্রতিটি ধাপে শেষে চলে যায়, এবং ধীরে ধীরে পুরো অ্যারে sort হয়ে যায়।  
> 
> 💡 যদি কোনো ধাপে একবারও swap না হয়, তাহলে বুঝতে পারি অ্যারে ইতিমধ্যেই sort হয়ে গেছে — তখন লুপ বন্ধ করে দেওয়া যায় (optimized version)।  
> 
> 🔁 সময় জটিলতা (Time Complexity):  
> Worst, Average: **O(n²)**  
> Best (already sorted): **O(n)** (with optimization)

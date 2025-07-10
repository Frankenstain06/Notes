## Math
---

### Permutation and Combination  
> What is the permutation of A B C?  
  It is: AB AC BA BC CA CB (order matters here) -> 6 permutation.  
  Formula: $\frac{n!}{(n-r)!}$ **->** **n** = 3 (numbers of item: A B C),  **r** = 2 (item to choose: AB).

>what is the combination of A B C?  
  It is: AB AC BC (order doesn't matters here) -> 3 combination.  
  Formula: $\frac{n!}{(n-r)! r!}$

### code:
```cpp
int factorial(int a){
    if(a == 1) return 1;
    else return a * factorial(a-1);
}
int permutation(int n, int r){
    int ans = factorial(n)/factorial(n-r);
    return ans;
}
int combination(int n, int r){
    int ans = permutation(n,r)/factorial(r);
    return ans;
}
```
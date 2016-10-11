## Power of two

Given an integer, write a function to determine if it is a power of two.

``` java
public class Solution {
public boolean isPowerOfTwo(int n) {
int result = 0;
if(n > 0){
result = n & n-1;
if(result == 0)
return true;
}
return false;
}
}
```

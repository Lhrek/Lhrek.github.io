---
layout:     post
title:      "CS106B Assignments1"
subtitle:   "Getting Your C++ Legs （2024.spring）"
date:       2024-06-03 11:08:51
author:     "GanZJ"
header-img: "img/post-bg-cs106b.jpeg"
catalog: true
tags:
  - cs106b
---

## Perfect numbers

```cpp
long smarterSum(long n) {
    /* TODO: Fill in this function. */
    long total = 0;
    for(long divisor = 1; divisor <= sqrt(n); divisor++){
        if(divisor == 1 || divisor == sqrt(n))
            total += divisor;
        else if ( n % divisor == 0)
            total = total + divisor + n/divisor;
    }
    return total;
}
```



```cpp
long findNthPerfectEuclid(long n) {
    if (n < 1 )
        return -1;

    long count = 1;
    long k = 1;
    do{
        long m = pow(2,k) - 1;
        if (smarterSum(m) == 1 && count == n)
            return pow(2,k-1) * (pow(2,k) - 1);
        if (smarterSum(m) == 1){
            count ++;
        }
        k++;
    }while(true);

    return -1;
}
```



```c++
STUDENT_TEST("Multiple time trials of findPerfects on increasing input sizes") {
   int smallest = 20000, largest = 160000;
   for (int size = smallest; size <= largest; size *= 2) {
       TIME_OPERATION(size, findPerfects(size));
   }
   EXPECT(!isPerfect(-6));
   EXPECT(!isPerfect(-5));
   EXPECT(!isPerfect(-4));
}

STUDENT_TEST("Multiple time trials of findPerfects on increasing input sizes") {
   int smallest = 20000, largest = 160000;
   for (int size = smallest; size <= largest; size *= 2) {
       TIME_OPERATION(size, findPerfectsSmarter(size));
   }
}

STUDENT_TEST("Confirm smarterSum is corrent"){
    EXPECT_EQUAL(smarterSum(25),6);
    EXPECT_EQUAL(smarterSum(100),divisorSum(100));
    EXPECT_EQUAL(smarterSum(-100),divisorSum(-100));
}

STUDENT_TEST("Confirm findNthPerfectEuclid is corrent"){
    EXPECT_EQUAL(findNthPerfectEuclid(1),1);
    EXPECT_EQUAL(findNthPerfectEuclid(3),28);
    EXPECT_EQUAL(findNthPerfectEuclid(5),8128);
    EXPECT_EQUAL(findNthPerfectEuclid(-1),-1);
    EXPECT_EQUAL(findNthPerfectEuclid(9),
                 2305843008139952128);
}

```



## 

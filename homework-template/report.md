# 41443115

# 作業一

# Problem 1：Ackermann's Function

## 解題說明

#### 問題描述

本題要求我寫出阿克曼函數並寫兩種版本：
1. 遞迴
2. 非遞迴

#### 解題策略

1. **遞迴版本 ：** 
   直接對應數學定義的三個條件自我呼叫就好。

2. **非遞迴版本** ：
   需手動模擬遞迴
   * 將當前的 $m$ 推入堆疊，變數 $n$ 作為當前數值。
   * 遇到 $m = 0$ 時計算 $n = n + 1$。
   * 遇到 $n = 0$ 時將 $m - 1$ 推入堆疊，重設 $n = 1$。
   * 遇到一般情況時，先將外層的 $m - 1$ 推入堆疊，再將內層的 $m$ 推入堆疊，並將 $n$ 減 1，藉由後進先出的順序依序解開計算。

## 程式實作

#### 遞迴版本 (`problem1/algorithm1.cpp`)

```cpp
#include <iostream>
using namespace std;

int ack(int m, int n) {
    if (m == 0) 
        return n + 1;
    else if (n == 0) 
        return ack(m - 1, 1);
    else 
        return ack(m - 1, ack(m, n - 1));
}

int main() {
    int m1, n1;
    cin >> m1 >> n1;
    cout << ack(m1, n1) << endl;
    return 0;
}

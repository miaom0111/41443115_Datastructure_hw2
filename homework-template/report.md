# 41443115 作業一

## 解題說明

### Problem 1：Ackermann's Function
#### 問題描述
本題要求我寫出阿克曼函數並寫兩種版本：
1. 遞迴
2. 非遞迴

#### 解題策略
1. **遞迴版本**：
   直接對應數學定義的三個條件自我呼叫就好。
2. **非遞迴版本**：
   需手動模擬遞迴
   * 將當前的 $m$ 推入堆疊，變數 $n$ 作為當前數值。
   * 遇到 $m = 0$ 時計算 $n = n + 1$。
   * 遇到 $n = 0$ 時將 $m - 1$ 推入堆疊，重設 $n = 1$。
   * 遇到一般情況時，先將外層的 $m - 1$ 推入堆疊，再將內層的 $m$ 推入堆疊，並將 $n$ 減 1，藉由後進先出的順序依序解開計算。

### Problem 2：Powerset
#### 問題描述
若集合 $S$ 含有 $n$ 個元素，其冪集（Powerset）是包含 $S$ 的所有子集合的集合（包括空集合與自身）。
若集合元素個數為 $n$，其冪集的子集合總數必為 $2^n$ 個。

#### 解題策略
採用二元決策樹（Binary Decision Tree）與回溯概念進行遞迴搜尋：
1. 對於集合中的每一個元素，都有兩種可能：「**不選**」或「**選入**」。
2. 使用遞迴索引 `index` 依序推進。
3. 終止條件：當 `index` 達到集合大小 $n$ 時，表示所有元素皆已決定好狀態，將當前組合輸出。

## 程式實作

### Problem 1

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

# 41443115

## 解題說明

### Problem 1：Ackermann's Function
本題要求我寫出阿克曼函數並寫兩種版本：遞迴與非遞迴。
- **遞迴版本**：直接對應數學定義的三個條件自我呼叫。
- **非遞迴版本**：手動模擬遞迴，利用 `std::stack` 管理狀態，並依照條件將 $m-1$ 與 $m$ 推入堆疊中，直至算完所有狀態。

### Problem 2：Powerset
本題要求列出集合 $S$ 的冪集。
採用二元決策樹（Binary Decision Tree）與回溯概念進行遞迴搜尋，對每個元素進行「選」或「不選」的遞迴分支，直到所有元素決策完畢即可輸出。

## 程式實作

### Problem 1：遞迴與非遞迴版本
```cpp
#include <iostream>
#include <stack>
using namespace std;

// 遞迴版本
int ack_rec(int m, int n) {
    if (m == 0) return n + 1;
    else if (n == 0) return ack_rec(m - 1, 1);
    else return ack_rec(m - 1, ack_rec(m, n - 1));
}

// 非遞迴版本
int ack_iter(int m, int n) {
    stack<int> s;
    s.push(m);
    while (!s.empty()) {
        m = s.top();
        s.pop();
        if (m == 0) {
            n += 1;
        } else if (n == 0) {
            s.push(m - 1);
            n = 1;
        } else {
            s.push(m - 1);
            s.push(m);
            n -= 1;
        }
    }
    return n;
}

int main() {
    int m, n;
    cin >> m >> n;
    cout << ack_iter(m, n) << endl;
    return 0;
}

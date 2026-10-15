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
```

### Problem 2：Powerset
```cpp
#include <iostream>
using namespace std;

char S[] = { 'a', 'b', 'c' };
const int n = 3;
bool chosen[n];
bool isFirst = true;

void powerset(int index) {
    if (index == n) {
        if (!isFirst) cout << ", ";
        isFirst = false;
        cout << "(";
        bool firstElement = true;
        for (int i = 0; i < n; i++) {
            if (chosen[i]) {
                if (!firstElement) cout << ", ";
                cout << S[i];
                firstElement = false;
            }
        }
        cout << ")";
        return;
    }
    chosen[index] = false;
    powerset(index + 1);
    chosen[index] = true;
    powerset(index + 1);
}

int main() {
    cout << "powerset(S) = {";
    powerset(0);
    cout << "}" << endl;
    return 0;
}
```

## 效能分析

### Problem 1
- **時間複雜度**：無法以多項式表示。當 $m \ge 4$ 時，計算次數急遽膨脹。
- **空間複雜度**：遞迴版本取決於系統 Call Stack 的深度；非遞迴版本取決於 `std::stack` 最大儲存元素個數。

### Problem 2
- **時間複雜度**：$O(n \times 2^n)$。共有 $2^n$ 個子集合，需遍歷長度為 $n$ 的陣列。
- **空間複雜度**：$O(n)$。遞迴最大深度為 $n$。

## 測試與驗證

### Problem 1
- 輸入 `2 3`，預期輸出 `9`，實際輸出 `9`。
- 輸入 `3 2`，預期輸出 `29`，實際輸出 `29`。
遞迴與非遞迴版本測試結果皆正確。

### Problem 2
- 輸入 `{a, b, c}`
- 輸出：`powerset(S) = {(), (c), (b), (b, c), (a), (a, c), (a, b), (a, b, c)}`
共 8 個子集合，完整包含所有組合且無重複，符合預期。

## 申論及開發報告

本次作業聚焦於遞迴思維與堆疊的應用。在 Problem 1 實作阿克曼函數的過程中，我深入理解了遞迴的本質，並學會如何使用堆疊手動模擬遞迴，這讓我對編譯器底層處理函式呼叫的機制有更深刻的認識。

在 Problem 2 中，利用分枝遞迴解決了 Powerset 窮舉問題。這讓我掌握了二元決策樹的邏輯，並學會透過陣列來記錄遞迴狀態，避免不必要的字串操作，使程式碼更為簡潔且易於維護。

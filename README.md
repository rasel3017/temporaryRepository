#include <iostream>
#include <queue>
using namespace std;

int main() {
    // Fast I/O to handle up to 100k numbers
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int n;
    cin >> n;

    priority_queue<long long> maxHeap;   // max-heap (default)

    for (int i = 0; i < n; ++i) {
        long long x;
        cin >> x;
        maxHeap.push(x);

        if (i < 2) {
            cout << "-1\n";
        } else {
            // Extract the three largest elements
            long long first  = maxHeap.top(); maxHeap.pop();
            long long second = maxHeap.top(); maxHeap.pop();
            long long third  = maxHeap.top(); maxHeap.pop();

            cout << first * second * third << "\n";

            // Put them back into the heap
            maxHeap.push(first);
            maxHeap.push(second);
            maxHeap.push(third);
        }
    }

    return 0;
}

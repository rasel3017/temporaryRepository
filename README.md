#include <iostream>
#include <queue>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int M, N;
    cin >> M >> N;

    priority_queue<int> pq;   // max-heap (default is less<int>, gives largest)

    for (int i = 0; i < M; ++i) {
        int seats;
        cin >> seats;
        pq.push(seats);
    }

    long long total = 0;   // total can be up to 10^12, so use long long

    for (int i = 0; i < N; ++i) {
        int best = pq.top();   // row with most empty seats
        pq.pop();

        total += best;

        if (best > 1) {
            pq.push(best - 1);  // one more seat filled, price drops by 1
        }
    }

    cout << total << '\n';

    return 0;
}

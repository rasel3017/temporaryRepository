#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    // Create a boolean array to mark which levels can be passed
    // Index 1 to n will be used (ignore index 0)
    bool can_pass[105];
    for (int i = 1; i <= n; i++) {
        can_pass[i] = false;
    }

    // Read levels that Little X can pass
    int p;
    cin >> p;
    for (int i = 0; i < p; i++) {
        int level;
        cin >> level;
        can_pass[level] = true;
    }

    // Read levels that Little Y can pass
    int q;
    cin >> q;
    for (int i = 0; i < q; i++) {
        int level;
        cin >> level;
        can_pass[level] = true;
    }

    // Check if all levels from 1 to n are marked as passable
    bool all_passed = true;
    for (int i = 1; i <= n; i++) {
        if (can_pass[i] == false) {
            all_passed = false;
            break;
        }
    }

    // Output the appropriate message
    if (all_passed) {
        cout << "I become the guy.";
    } else {
        cout << "Oh, my keyboard!";
    }

    return 0;
}

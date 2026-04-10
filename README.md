#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    // Arrays to store home and guest uniform colors
    int home[35];
    int guest[35];

    // Read data for each team
    for (int i = 0; i < n; i++) {
        cin >> home[i] >> guest[i];
    }

    int count = 0;

    // Check all pairs where one team hosts and another visits
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            // A team cannot play against itself
            if (i != j) {
                // If host's home color matches guest's guest color
                if (home[i] == guest[j]) {
                    count = count + 1;
                }
            }
        }
    }

    cout << count;

    return 0;
}

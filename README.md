#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;

    // Arrays to store problems solved and penalty time
    int problems[55];
    int penalty[55];

    // Read all teams' data
    for (int i = 0; i < n; i++) {
        cin >> problems[i] >> penalty[i];
    }

    // Sort teams using bubble sort
    // Teams with more problems solved come first.
    // If problems are equal, team with less penalty time comes first.
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            // Check if team j should come before team i
            bool should_swap = false;
            
            if (problems[j] > problems[i]) {
                // More problems solved -> higher rank
                should_swap = true;
            } else if (problems[j] == problems[i] && penalty[j] < penalty[i]) {
                // Same problems but less penalty -> higher rank
                should_swap = true;
            }

            if (should_swap) {
                // Swap problems
                int temp_problems = problems[i];
                problems[i] = problems[j];
                problems[j] = temp_problems;

                // Swap penalty
                int temp_penalty = penalty[i];
                penalty[i] = penalty[j];
                penalty[j] = temp_penalty;
            }
        }
    }

    // The k-th place team is at index (k - 1) in sorted array
    int target_problems = problems[k - 1];
    int target_penalty = penalty[k - 1];

    // Count how many teams have exactly the same score as the k-th team
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (problems[i] == target_problems && penalty[i] == target_penalty) {
            count = count + 1;
        }
    }

    cout << count;

    return 0;
}

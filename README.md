#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    // Vector to store names that have been seen before
    vector<string> seen;

    // Process each name one by one
    for (int i = 0; i < n; i++) {
        string name;
        cin >> name;

        // Check if the name already exists in the 'seen' list
        bool found = false;
        for (int j = 0; j < seen.size(); j++) {
            if (seen[j] == name) {
                found = true;
                break; // Stop searching once found
            }
        }

        // Output based on whether the name was found
        if (found) {
            cout << "YES" << endl;
        } else {
            cout << "NO" << endl;
            // Add the new name to the list for future checks
            seen.push_back(name);
        }
    }

    return 0;
}

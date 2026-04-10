#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    // If n is less than 2, there cannot be a second distinct value
    if (n < 2) {
        cout << "NO";
        return 0;
    }

    // Create an array (vector) to store the numbers
    vector<int> arr(n);

    // Read all numbers
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // Sort the array using simple bubble sort
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] > arr[j]) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    // Find the smallest value (first element after sorting)
    int smallest = arr[0];

    // Look for the first value greater than smallest (the second distinct)
    for (int i = 1; i < n; i++) {
        if (arr[i] > smallest) {
            cout << arr[i];
            return 0;
        }
    }

    // If we reach here, all numbers are the same
    cout << "NO";

    return 0;
}

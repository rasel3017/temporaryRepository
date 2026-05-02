#include <iostream>
#include <stack>
#include <string>
#include <map>

using namespace std;

string isBalanced(string s) {
    stack<char> st;
    map<char, char> matching = {{')', '('}, {'}', '{'}, {']', '['}};

    for (char c : s) {
        // If it's an opening bracket, push to stack
        if (c == '(' || c == '{' || c == '[') {
            st.push(c);
        } else {
            // It's a closing bracket
            if (st.empty() || st.top() != matching[c]) {
                return "NO";
            }
            st.pop();
        }
    }

    return st.empty() ? "YES" : "NO";
}

int main() {
    int n;
    cin >> n;
    cin.ignore(); // Ignore the newline after the integer

    for (int i = 0; i < n; ++i) {
        string s;
        getline(cin, s);
        cout << isBalanced(s) << endl;
    }

    return 0;
}

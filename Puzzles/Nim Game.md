Question:

Initially, there is a heap of stones on the table.

You and your friend will alternate taking turns, and you go first.

On each turn, the person whose turn it is will remove 1 to 3 stones from the heap.

The one who removes the last stone is the winner.

Given n, the number of stones in the heap, return `true` if you can win the game assuming both you and your friend play optimally, otherwise return `false`.


```
class Solution {
public:
    bool canWinNim(int n) {
        return n & 3;
    }
};
```
Logic:
It is not posiible for the player that is starting to win if the number of stones is divisible by 4 (3 + 1 => Since, players can pick stones ranging from `1 - 3`) and n % 4 == n & 3.

# Exp 12 - Detailed Analysis

## a) Final Hash Tables (m=10)

All keys: 23,43,13,33,53,63,73 all give h(k)=3

### Linear Probing
Index: 0 1 2 3 4 5 6 7 8 9
Value: - - - 23 43 13 33 53 63 73
Probes: 1,2,3,4,5,6,7 total 28 avg 4.0

### Quadratic Probing (m=10 FAILS)
Quadratic sequence for key hashing to 3:
i=0 ->3
i=1 ->5 (3+1+1)
i=2 ->9 (3+2+4)
i=3 ->5 again (3+3+9=15%10=5) loop
Only 4 distinct slots reachable -> fails after 3 insertions.
**Solution: Use prime m=11**

### Quadratic Probing (m=11) - SUCCESS
h(k): 23->1,43->10,13->2,33->0,53->9,63->8,73->7
Table (m=11):
0:33,1:23,2:13,7:73,8:63,9:53,10:43 (no collision actually! Shows benefit of prime)

If we force collision with m=10 using alternative h:
0:53,1:73,3:23,4:43,5:33,9:13 etc depending on c1,c2.

### Double Hashing (m=10)
h2(k)=7-(k%7): 23->5,43->6,13->1,33->2,53->3,63->7,73->4
Insert:
23 ->3
43 ->3+6=9
13 ->3+1=4
33 ->3+2=5
53 ->3+3=6
63 ->3+7=0 (3+7%10)
73 ->3+4=7
Table: [63, -, -,23,13,33,53,73, -,43]
Only 7 probes total avg 1.0 - BEST!

## b) Search Probes

| Key | Type | Linear | Quadratic(m11) | Double |
|-----|------|--------|----------------|--------|
| 33 | Exist | 4 | 1 | 1 |
| 73 | Exist | 7 | 1 | 1 |
| 83 | Not | 8 | 2 | 2 |
| 99 | Not | 8 | 2 | 2 |

Double hashing clearly wins.

## c) Load Factor α = n/m

α=0.7 (high)

As α increases:
- Linear degrades fastest O(1/(1-α)^2)
- Quadratic moderate
- Double hashing best O(1/(1-α))

## Conclusion

For railway booking where booking IDs may have pattern (ending with same digit),
Double Hashing is most suitable because probe step depends on key itself,
preventing clustering.

CO1, CO3, CO4 mapping: Hashing concepts, collision resolution, performance analysis.
L4: Analyze level.

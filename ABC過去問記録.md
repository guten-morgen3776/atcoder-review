# ABC過去問記録
### ABC 429
- A: AC
- B: AC
  「一つでも満たせばOK」の処理でのbreak,continueの書き方が怪しい</br>
```
for i in range(N):
  if sum(A) - A[i] == M:
    print('Yes')
    break
  else:
    continue
else:
  print('No')
```
- C: TLE
  「リストの３つの要素のうち２つだけが等しい」という条件　普通に書いたらタイムオーバーだった　</br>
  出現回数に注目したら上手く行った　「愚直にやって無理なら数学的考察が必要」
```
from collections import Counter

N = int(input())
A = list(map(int, input().split()))

cnt = Counter(A) #要素の出現回数を辞書形式で出力
ans = 0
for c in cnt.values():
    if c >= 2:
      ans += c * (c - 1) // 2 * (N - c)
print(ans)
```

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
  「リストの３つの要素のうち２つだけが等しい」という条件　普通に書いたらタイムオーバーだった　

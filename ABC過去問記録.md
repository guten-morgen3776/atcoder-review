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
### ABC 428
- A: AC
- B: わからん</br>
特定の文字列内での長さ固定文字列の出現頻度 → 文字列＋出現回数の辞書を作る　でも辞書の使い方かなり怪しい</br>
```
dict['文字列'] = 対応する数値
dict.values(): 辞書内の数値全部
dict.items():辞書内の文字列と数値のセット全て
```
```
A.append(a) リストAに要素aを加える
```
- C: わからん</br>
「直接数式化しにくい条件は具体値で実験しよう」「受験数学の場合の数・確率を思い出せ」
### ABC 427
- A: AC
```
文字列のスライス処理
x = str(x)
x[:2] 文字列の０〜1まで #終端は含まない！！
x[3:] 文字列の3~最後まで
x[2:4]　文字列の２〜３まで
```
- B: AC
- C: わからん</br>
グラフ問題わからん
```
グラフ問題のインプット
N, M = map(int, input().split()) #N:頂点, M:辺
edges = [tuple(map(int, input().split())) for _ in range(M)]
# ノード間のエッジ情報をタプル形式でインプット
```
```
二部グラフ判定のアルゴリズム
ある頂点を赤に塗る
隣接する頂点を青に塗る
それに隣接する頂点を赤に塗る　・・・
それを続けていって同じ色同士が繋がっていたらアウト
```
```
def check_bipartite(N, edges):
  color = [0] * (N + 1) #リストの０は使わない
  for start in range(1, N + 1):
    if color[start] == 0: #色がついてない頂点を見つけて赤に塗る
      color[start] = 1
    for u, v in edges:
      if u == start and color[v] == 0:
        color[v] = 3 - color[u] #赤の隣には青、青の隣には赤
      elif v == start and color[u] == 0:
        color[u] = 3 - color[v]
  for u, v in edges:
    if color[u] == color[v]:
      return False #同じ色同士をむすぶ辺があったらアウト
  return True
```
```
delete = []
from itertools import combinations 
for i in range(0, M + 1): #i本消す場合を考える
  for removed in combinations(range(M), i):
    #combination関数で範囲内からi個取るパターンを列挙
    new_edges = []
    for j in range(M):
      if j not in removed:
        new_edges.append(edges[j])
    if check_bipartite(N, new_edges):
      delete.append(i)
print(min(delete))
```
こんな感じで全探索したんだけどTLEになっちまった😭 後で考え直す
### ABC 057 C
普通に書くとTLEになる
```
約数探索
１〜Nで全探索するより
１〜√Nで全探索してペアを考えた方が計算量のオーダーを減らせる
```
```
10 ** nとかで挟むより
文字列に変換してlen()でやったほうが圧倒的に計算量減らせる!!
```
### https://atcoder.jp/contests/sumitrust2019/tasks/sumitb2019_d
```
パターン列挙ツール
#itertoolsの使い方
combinations([1,2,3,4,5],3) :リストから３つ選ぶパターンを全列挙
```
```
 set() :リスト内の要素を重複なく抽出
```
普通にN個から３つ取り出す順列を全列挙してると計算量が多すぎる</br>
→***片方を固定してパターン数が少ない方で全探索！！***
３つの並び方のパターンは少ない→３桁候補を固定してそれが存在するか調べる
```
f-stringの書き方
文字列内に直接変数を埋め込める
f"適当な文字列{変数}"
```
### ABC 424 
c: WA
伝播問題　普通にループを組むと拾いきれない→別のアルゴリズムが必要
```
参考　https://qiita.com/drken/items/996d80bcae64649a6580
BFS（幅優先探索）の考え方
各ノードおよびノード間のエッジ情報からグラフを作成
→

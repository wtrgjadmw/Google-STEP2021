![#1589F0](https://via.placeholder.com/15/1589F0/000000?text=+) `#1589F0`

## 宿題 1

eval_part という関数を追加した。

### eval_part の仕様

以下の 1〜3 を行うことで**tokens: 1 + 2\*3 + 4/2** を **new_tokens: 1 + 6 + 2** に変換する。

1. 空の配列 new_tokens，変数 index・tmp を用意する。<br/>
   eval_part 内の index は，式の中の符号の位置を表す。上の例では，最初の符号は 1+...の+なので，index=1
   (もし式が-から始まっていたら(ex. -1 + 2\*3)，index=2)から始まる。その後， tokens の中身を見ていくと 2 つおきに符号が来るはずなので，ループするごとに index に 2 を足していく。<br/>
   また，変数 tmp で式の中のかけ算・わり算の結果を保持する。<br/>

2. tokens の中身を見ていく。<br/>

- tokens[index]が+または-なら tmp と token[index]を new_tokens に追加する。
- tokens[index]が\*または/なら tmp にかけ算・割り算を行う。
- index += 2

3. 2 を繰り返して tokens を最後まで参照したら，最後に保持している tmp を new_tokens に追加する。

具体例 (1 + 2\*3 + 4/2) を使って流れを見ていく。

---

index = 1, tmp = 1 <span style="color: #1589F0;">-> 2</span><br/>
tokens: 1 <span style="color: #1589F0;">+</span> 2 \* 3 + 4 / 2<br/>
new_tokens: <span style="color: #1589F0;">1 +</span>

---

index = 3, tmp = 2 <span style="color: #1589F0;">-> 6 (2 * 3)</span><br/>
tokens: 1 + 2 <span style="color: #1589F0;">_</span> 3 + 4 / 2<br/>
new_tokens: 1 +

---

index = 5, tmp = 6 <span style="color: #1589F0;">-> 4</span><br/>
tokens: 1 + 2 \* 3 <span style="color: #1589F0;">+</span> 4 / 2<br/>
new_tokens: 1 + <span style="color: #1589F0;">6 +</span>

---

index = 7, tmp = 4 <span style="color: #1589F0;">-> 2 (4 / 2)</span><br/>
tokens: 1 + 2 \* 3 + 4 <span style="color: #1589F0;">/</span> 2<br/>
new_tokens: 1 + 6 +

---

ループ脱出<br/>
new_tokens: 1 + 6 + <span style="color: #1589F0;">2</span>
→終了。new_tokensを返す

## 宿題 2



## 宿題 3

関数update_tokensとreadBracketsを追加した。

### update_tokensの仕様

関数tokenizeのwhileの中身をmodule化しただけのもの

### readBracketsの仕様

lineを読み込み，()の中身を計算して，type = NUMBER のtokenを返す。

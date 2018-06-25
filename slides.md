# メールの文字化け

NSEG #101

2018/06/30

とみたまさひろ

---

## 自己紹介

* とみたまさひろ
* 長野在住プログラマー
* 得意技
  * Ruby
  * MySQL
  * 文字化け

---

一般的な文字化けの原因

---

書き手の文字コードと読み手の文字コードが異なる

---

文字コード

---

文字集合

文字エンコーディング

---

文字集合

Character set

文字の集まり

ASCII
JIS X 0201 / 0208 / 0213
Windows-31J
Unicode

---

文字エンコーディング

文字の符号化方式

ISO-2022-JP
EUC-JP
SHIFT_JIS
UTF-8
UTF-16

---

全体的に文字化けする場合

---

エンコーディングが異なる

アプリが対応していないエンコーディング

---

単純なテキストファイルはエンコーディング情報を持っていない

テキストエディタ等のアプリが推測したり

---

ある文字だけ文字化けする場合

---

文字集合が異なる

Windows-31J = JIS X 0201 + JIS X 0208 + α

---

文字集合のバージョンが異なる

JIS X 0208-1983
JIS X 0208-1990
JIS X 0208-1997

---

データが壊れている

フォントが対応していない

---

メールの場合

---

charsetと本文が異なる

```
Content-Type: text/plain; charset=ISO-2022-JP

なぜか本文はSHIFT_JIS
```

---

Subjectが生ISO-2022-JP

```
Subject: ^[$B%"%a%s%\@V$$$J$"$$$&$($*^[(B
```

MIME以前はこんな感じだった。

---

添付ファイル名がMIMEヘッダエンコーディング(RFC2047)

```
Content-Type: application/octet-stream;
  name="=?UTF-8?B?44G744GSLnhscw==?="
```

本当は規約違反。今でも結構ありそう。
MIME登場後もしばらくは日本語ファイル名をつけられなかった。

---

ただしくは RFC2231

```
Content-Type: application/octet-stream;
  name*=utf-8''%E3%81%BB%E3%81%92.xls
```

でもこのRFCにはerrataがあった。
昔のThunderbirdは間違ってるので実装したりしてた。

---



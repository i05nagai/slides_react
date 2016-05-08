class: center, middle

# Summary of Windowsの使い方基礎編 via COM and .NET Framework

---

### 大事なこと

Windowsはオブジェクト指向が大好き
* Microsoft純正のものはオブジェクトとして操作できることが多い

---

### Component Object Model
COMはオブジェクト指向と親和性のあるdllを作る技術。
動的ライブラリ(dll)をOSやコンパイラに依存しない形で利用できるように、Microsoftが策定した仕様。
オブジェクト指向プログラミングの（ある意味の）一般化。

### dllの問題
* 作ったライブラリは同じ言語、コンパイラ、OSでないと再利用できない(ことが多い、多かった)
    * 動的ライブラリの意味がない
* クラスのインターフェースが不変でも、dllが再利用できない（ことが多い、多かった）
    * オブジェクト指向の意味がない

### COMが作られた経緯
* 作ったライブラリをdllとして配布したいわー
* dllごみやな
* dllがライブラリとして使えるような仕組みを作ったろ

---

### Object Linking and Embedding(OLE)
COMを作って、ExcelやWordなどをオブジェクトとして操作できるような仕組みがOLEとして提供された。
エクセル表のwordへの埋め込みなどはOLEで行われている。
####ExcelやWordはプログラムで操作可能

### COMが使われているもの
20年以上前からずっと、アプリケーションをオブジェクトとして提供するということをやっているのでWindowsにはいっぱいある。
* Excel, WordなどのOLE由来のもの
* Visual Studio
* Internet Explorer
* ActiveX
    * Adobe PDF Reader
など。

---

### .NET Framework
COMはOSやコンパイラに依存しないという目的の為に作られた。
この目的をCOMより上手く実現した言語がJava

Javaの仕組みは
1. Javaのコードを**OSやCPUに依存しない機械語程度に低級な中間言語**といわれるコードに変換
2. 仮想環境上で、実行時に中間言語を機械語に変換して実行

.NET Frameworkは
1. ある言語(C#, C++/CLI, VB.NETなど）のコードを**OSやCPUに依存しない中間言語(IL)**といわれるコードに変換
2. 仮想環境上(CLR)で、実行時に中間言語(IL)を機械語に変換して実行

#### .NET FrameworkはJavaのぱくり。

---

### .NET Frameworkが使われているもの
かなりいっぱいある。
以前はCOMでかかれていたものも.NET Frameworkで実装されていることが多い。
* Excel, WordなどのOLE由来のもの
* Visual Studio
* Internet Explorer

使い道としては
* .NET Frameworkのライブラリでエクセル操作
* .NET FrameworkからCOMを経由してエクセル操作

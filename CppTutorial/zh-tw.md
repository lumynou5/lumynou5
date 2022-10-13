---
title: 現代 C++ 101
tags: Tutorial
lang: zh-tw
breaks: false
---

:::warning
WIP！
:::

# 序

C\+\+ 是一個強大的程式語言，儘管名字上相似，也有歷史淵源，但 C\+\+ 並非 C 的超集，如同Javascript 之於 Java，應該作為不同的語言看待。
其能夠在兼顧高效能的同時表達高階概念，輕鬆撰寫出跨平台的程式碼，因而歷久不衰。
無論是初學者，抑或已經掌握其他語言的程式設計師都適合學習。

## 致謝

感謝一路上幫助我的人們，在我曾經迷茫無知的時候伸出援手，沒有他們我不可能變成現在的樣子。
希望這份教學可以帶領更多人，在資訊的世界翱遊，而不迷失方向。

# 入門

C\+\+ 是一種預先編譯的語言，這表示你必須先把你的程式碼（原始碼）*編譯*成執行檔。如此一來，若你想要分享你的程式，可以直接發送執行檔而不是要求其他人安裝執行環境（例如 Python）。

這個章節中，我們將討論如何安裝必要的工具，以及撰寫第一個程式。

## 安裝

為了撰寫程式，你至少需要：

- 編輯器（editor）
- 編譯器（compiler）

如果你正在進行一個大型專案，你甚至需要更多工具！（當然你也可以靠自己的大腦）

編輯器就是任何可以編輯檔案的應用程式，例如記事本；編譯器則是「將原始碼翻譯成電腦可以執行的 0 和 1」的程式。

所以，你可以使用 Windows 的記事本來寫程式，但那很不方便，因此開發者通常會使用整合開發環境（integrated development environment，IDE），一個好的 IDE 甚至可以讓你開發得更有效率。
我推薦使用 JetBrains 的 [CLion](https://www.jetbrains.com/clion/)[^CLion]，或者你也可以選擇其他的，如 [Microsoft Visual Studio](https://visualstudio.microsoft.com/zh-hant/) 等。

IDE 通常有許多強大的輔助功能，但那不是我們要討論的。
因此，這裡將（假設你）使用一個普通的文字編輯器和終端來手動編譯，當然你也可以透過 IDE 的 GUI 操作，你可以在它們的網站上找到說明。

接著，要安裝一個 C\+\+ 編譯器，Windows 中可以安裝 [clang](https://github.com/llvm/llvm-project/releases)，Linux 則可以使用 [g++](https://gcc.gnu.org/)，當然這兩個實作其實都支援很多平台，也還有很多其他的編譯器，這只是建議而已。

## 程式進入點

一個函式（function）的定義包含四個部分：回傳型別（return type）、名稱（name）、參數（parameter）、主體（body）。
這裡的函式比起數學上的函數，稱作子程式可能更爲恰當，你可以傳入引數（argument）來呼叫函式，並得到回傳值。
但有時更重要的是函式的副作用（side effect），這也是函式與數學函數最大的差異；例如我們常常要在螢幕上顯示文字，那就可以把這個動作包裝成一個函式，如此一來要顯示文字只要呼叫這個函式即可，而不用撰寫重複的流程。

進入點（entry point）是一個會在程式執行時，被系統呼叫的函式。在 C\+\+ 中這個函式通常是一個名稱為 `main`，會回傳一個 `int`（也就是整數，integer）的函式。
這個整數會回傳給函式的呼叫者——系統，通常以0表示程式成功執行完畢，其他數值的含義則由系統決定。

在下面的範例中，包含了一個函式，有回傳型別 `int`、名稱 `main`、參數（不接收參數），以及函式主體。
主體以花括號包裹，裡面是多個述句（statement）。
這個範例中只有一個述句：`return 0;`，也就是回傳 `0`。

<pre>
<code><div class="wrapper">
<div class="gutter linenumber"><span data-linenumber="1"></span>
<span data-linenumber="2"></span>
<span data-linenumber="3"></span>
</div>
<div class="code"><span class="token keyword">int</span> <span class="token function">main</span>() {
    <span class="token keyword">return</span> <span class="token number">0</span>;
}
</div></div></code></pre>

## 編譯並執行

打開文字編輯器，輸入上面的程式碼（原始的程式碼通常稱作原始碼（source code））並儲存成 `main.cpp`。然後打開終端，輸入：

<pre>
<code><span class="token function">g++</span> -std=c++17 -o main main.cpp
<span class="token function">chmod</span> +x main <span class="token comment"># 賦予檔案執行權限。</span>
<span class="token function">./main</span>
</code></pre>

`-std=c++17` 意味著使用 C\+\+17 標準編譯，這是此教學將採用的標準。
`-o` 則指定了輸出的檔案名稱。

注意指令會因為 shell 和編譯器而有所不同，請自行查找使用方式。

:::info
儘管在一些平台上，副檔名並非必須的，然而為了方便知道檔案的類型還是建議加上。

C\+\+ 原始碼常見的副檔名包括 `.cpp` 和 `.cc`。
:::

## Hello World

<pre>
<code><div class="wrapper">
<div class="gutter linenumber"><span data-linenumber="1"></span>
<span data-linenumber="2"></span>
<span data-linenumber="3"></span>
<span data-linenumber="4"></span>
<span data-linenumber="5"></span>
<span data-linenumber="6"></span>
</div>
<div class="code"><span class="token keyword">#include</span> <span class="token string">&lt;iostream&gt;</span>

<span class="token keyword">int</span> <span class="token function">main</span>() {
    <span class="token namespace">std</span>::<span class="token gvariable">cout</span> << <span class="token string">"Hello World!"</span>;
    <span class="token keyword">return</span> <span class="token number">0</span>;
}
</div></div></code></pre>

前置處理器會在編譯之前執行前置處理器指令（preprocessor directive），也就是井號開頭的行。
`#include` 指令能要求前置處理器找到指定的檔案，然後把裡面的內容貼上到你的檔案。
這裡，我們引入 了 C\+\+ 標準庫中的 `iostream`，這個檔案裡有一些輸出輸入相關的東西。
通常這些檔案被稱作標頭檔（header file）。

`std` 是一個命名空間（namespace），標準庫的東西都在這個命名空間中，如此一來就可以防止「撞名」。
例如假如有兩個地方都叫紐約，說「美國，紐約」就可以知道是哪個紐約了。
`::` 這個運算子能夠從命名空間中取得東西，所以 `std::cout` 就是「`std` 裡的 `cout`」的意思。

`cout` 的意思是 character output，連結到標準輸出流（standard output stream），通常會輸出到終端。

如果你會其他語言的話，或許會覺得 `<<` 很怪，那看起來是個位元左移運算子。
事實上，那是多載過的運算子，運算子就只是個函式，但讓程式碼更清楚（例如可以使用 `one < another` 而不用像 `one.isLessThan(another)` 這樣冗長）。
在這裡，`<<` 是「流出」，它將右方的值放到左方的流中。

而 `"Hello World!"` 是一個字串字面值（literal）。
在 C\+\+ 中，字串字面值必須使用雙引號包裹。

## 註解

註解（comment）是程式中的「筆記」，能夠讓人更快速的瞭解程式的意圖，而編譯器會忽略這些部分。

可以使用兩個斜線來標記註解的開始，直到該行結束都會被編譯器忽略。
從 `/*` 到第一個 `*/` 為止的內容也都會被忽略。
然而為了統一風格，Google style 建議只用其中一種，而不要混用。

<pre>
<code><span class="token comment">// 這是一行註解。</span>

<span class="token comment">/* 這是一「塊」註解。 */</span>
</code></pre>

:::info
註解的習慣十分重要！良好的註解可以讓其他人更快讀懂程式的意圖，也可以讓未來的自己更好維護。
:::

## 使用變數

當需要儲存一個值時，可以使用變數（variable）。
對於大多數如 C\+\+ 一樣的命令式語言來說，變數和數學上的變數並不一樣，更像是一個在代表記憶體上特定的空間（即物件，object）的名字。
最大的差異便是它是可變的（mutable）。

<pre>
<code><span class="token keyword">int</span> variable = <span class="token number">0</span>;
</code></pre>

例如上面的程式碼定義了一個名為 `variable` 的變數，其型別為 `int`，也就是說物件是一個整數。
在 C\+\+ 中型別決定了能做的運算，例如對整數可以進行加法。

變數的名字和程式中其他的名字，或者稱作「識別符（identifier）」，都必須符合 `/[A-Za-z0-9_]*/`，也就是說只能包含大小寫字母、數字和底線，不能以數字開頭，不和任何關鍵詞一樣。
實際上，C\+\+ 標準允許使用大部分的字元，但很多編譯器實作不支援，且使用其他語言不方便編寫，也不方便他人閱讀，因此不建議使用。

區域變數（local variable），也就是在函式主體內定義的變數，若是內建型別的話，預設初始化並不會決定它的值，嘗試取得資料是未定義行為（undefined behavior，UB）。
因此建議初始化所有變數。

### 內建型別

C\+\+ 提供的內建型別（built-in type）包含了算術型別和一些特別的型別，算術型別中又有許多整數型別（integral type）。

#### 整數型別

基礎的整數型別是 `int`，標準保證至少有16位元長，可以使用以下修飾符（modifier）：

- 有號性

  `signed`
  : 有號，預設的有號性。
  
  `unsigned`
  : 無號，即只能表示 0 和正數。
  
- 大小（通常會省略 `int`）

  `short`
  : 至少 16 位元。
  
  `long`
  : 至少 32 位元。
  
  `long long`
  : 至少 64 位元。

也可以將 `short`、`int`、`long`、`long long` 和其各自的無號版本視作不同型別，方便理解。

##### 字元型別

`char` 則是字元型別，但也是整數型別的一種。
然而並不建議用來當作整數運算，因為型別對程式設計師來說也決定了預期的資料類型，例如一個印出內容的函式可能會將字元型別的參數作為字元印出而非整數。

`char` 也可以使用 `signed` 和 `unsigned` 修飾，但如同前面所述，並不建議將其看作數字，若需要一個小的整數可以使用 `std::int8_t` 和 `std::uint8_t`。
預設的有號性是實作定義的。

寬字元（`wchar_t`，wide character）的大小至少能儲存機器所支援的任何編碼碼點。

`char8_t`<span class="lmn-va">（C\+\+20 後）</span>、`char16_t`、`char32_t` 則分別儲存 UTF-8、UTF-16、UTF-32 編碼下的一個編碼單元。
這表示除了 `char32_t`，其他兩個型別的物件可能不代表一個字元。

##### 布林型別

`bool` 表示一個布林值（boolean），即只有「是」和「否」兩種狀態的型別，字面值分別是 `true` 和 `false`。

#### 浮點數型別

`float`、`double`、`long double` 分別是不同精度的浮點數（single-precision、double-precision 和 extended-precision floating-point），浮點數是以二進位方式表示實數的近似值，因此存在誤差。

`float` 的精度最差，但所佔空間也較小，運算速度也較快，但得益於現代電腦效能的提升，這些差異有時並不明顯。

#### Void型別

還有一個特殊的型別：`void`。
其並不能作為變數的型別，用途也很少，最常見的用法是作為函式回傳型別表示沒有回傳值。
但請注意這不表示函式不會回傳（如永不型別），流程仍然會在回傳後回到呼叫的地方繼續執行，僅僅是沒有值被回傳而已。

#### Size-of 運算子

為了知道型別的大小可以使用 `sizeof` 運算子，例如 `sizeof(int)` 在一些機器上會回傳 4，也就是說一個 `int` 有四個 `char` 的大小。
其括號不一定要放型別，也可以是變數等。

### 參考

參考（reference）是一個物件的「別名」，本身並不是一個物件，使用上如下所示，型別後加上 `&` 即可。

<pre>
<code><span class="token keyword">int</span> i = <span class="token number">0</span>;
<span class="token keyword">int</span>&amp; ref = i;
</code></pre>

當定義一個參考變數時，必須將其繫結（bind）到一個變數，也就是告訴編譯器這個參考是哪個變數的別名，之後無法再改變繫結的對象。
對 `ref` 的所有操作都等同於對 `i` 進行的。

### 指標

指標（pointer）是一種儲存著記憶體位址（address）的變數，只要在型別後加上 `*` 表示指向前面的型別的物件的指標，例如 `int*` 表示指向一個 `int` 物件的指標、`int**` 表示指向一個 `int*` 物件的指標。

要取得物件的位址可以使用取址運算子（address-of operator）`&`，要取得指向的物件則可以使用間接取值運算子（indirection operator）`*`。

<pre>
<code><span class="token keyword">int</span> i = <span class="token number">0</span>;
<span class="token keyword">int</span>* ptr = &amp;i;
*ptr = <span class="token number">10</span>;
</code></pre>

:::info
未初始化的指標的值是未定義的，若嘗試取值將造成嚴重錯誤。
所有指標都應該被初始化。
:::

#### 未知型別的指標

有一個特殊的指標型別：`void*`，其指向的記憶體位置是什麼型別的物件是不固定的，因此也無法對其進行取值，因為並不知道物件的大小。

這個型別並不建議使用，大部分時候也不需要用，除非確定自己在做什麼，否則不要撰寫這樣的程式碼。

#### 指標的運算

指標可以進行加和減的運算，表示指標後或前的物件，例如 `ptr + 1` 表示 `ptr` 往後一個位置的物件。

#### 迷途指標

迷途指標（dangling pointer，又稱懸空指標、野指標）指向的記憶體位址是無效的，就好像迷途一樣，所謂無效指是像 `ptr + 1` 這樣。
`ptr` 指向的是 `i`，那 `i` 後面一個位置是什麼？

#### 空指標

如果一個指標不指向任何東西，或者說指向「沒有東西」，可以使用字面值 `nullptr`，這個特殊的值可以隱式轉換成任何型別的指標。
如此一來，便可以用 `if (ptr)` 等方式來檢查，而不會有未初始化的指標的問題。

嘗試從「沒有東西」取值是未定義行為。

### 陣列

陣列是一種使用一個變數來存取多個物件的方式，也就是說，可以只用一個陣列變數來表示一連串同型別的資料，而不用多個變數。

<pre>
<code><span class="token keyword">int</span> arr[<span class="token number">3</span>]; <span class="token comment">// `arr` 有 3 個整數元素，其值未定義。</span>
</code></pre>

可以使用初始化列表來初始化陣列元素的值。
如果有初始化，也可以讓編譯器自行推導陣列長度：

<pre>
<code><span class="token keyword">int</span> arr[] = {<span class="token number">10</span>, <span class="token number">20</span>, <span class="token number">30</span>}; <span class="token comment">// `arr` 的長度為 3。</span>
</code></pre>

然而傳統陣列也有許多缺點，例如無法一次存取整個陣列：

<pre>
<code><span class="token keyword">int</span> a[] = {<span class="token number">10</span>, <span class="token number">20</span>, <span class="token number">30</span>};
<span class="token keyword">int</span> b[] = a;            <span class="token comment">// 錯誤，陣列只能使用預設初始化或列表初始化。</span>
a = {<span class="token number">50</span>, <span class="token number">60</span>, <span class="token number">70</span>};       <span class="token comment">// 錯誤，初始化列表並不是建構一個陣列。</span>
</code></pre>

要存取陣列中的元素，可以使用下標運算子（subscript operator）`[]`。
值得注意的是索引（index）是從 0 開始的，且*沒有超界檢查*（一些編譯器實作可能會警告）。

<pre>
<code><span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; arr[<span class="token number">0</span>];
</code></pre>

`sizeof` 運算子會回傳陣列大小相當於多少個 `char`，就像對其他型別一樣，因此對於一個長度為 3 的 `int` 陣列，在 `int` 是 4 個 `char` 的情況下，會得到 12。

#### 陣列與指標的轉換

在需要指標的地方給陣列，會隱式轉換為指標，指向陣列中第一個物件。
因此，`arr[idx]` 的效果等同於 `*(arr + idx)`，陣列會轉換成指標再透過指標加法取得其後第 `idx` 個物件的位址並取值。

另外，`arr` 會隱式轉換成第一個元素的位址，型別是 `int*`，但 `&arr` 是取得陣列的位址，因此型別是 `int(*)[length]`。

<pre>
<code><span class="token keyword">int</span> arr[<span class="token number">3</span>] = {<span class="token number">10</span>, <span class="token number">20</span>, <span class="token number">30</span>};
<span class="token keyword">int</span>* ptr0 = arr;
<span class="token keyword">int</span>* ptr1 = &amp;arr;          <span class="token comment">// 錯誤，`int(*)[3]` 無法轉換至 `int*`。</span>
<span class="token keyword">int</span>(* ptr2)[3] = &amp;arr;
</code></pre>

### 字面值

所謂字面值（literal）便是寫死在程式碼中的值，例如 `0` 是一個 `int` 型別的字面值。

整數字面值後可以加上後綴，來指定型別（預設是 `int`）。
後綴不分大小寫，但通常使用大寫，因為字母 `l` 和數字 `1` 外形相似。

| 後綴 | 型別        |
| ---- | ----------- |
| `U`  | `unsigned`  |
| `L`  | `long`      |
| `LL` | `long long` |

例如，`10UL` 是一個 `unsigned long` 型別的整數。

也可以加上前綴來改變進位制，一般是十進位，`0x` 開頭的數字則是十六進位，`0` 開頭的數字是八進位。

---

只要數字中包含小數點，預設型別便是 `double`。
若字面值沒有小數位，但想使用 `double` 型別，可以加上小數點，如 `10.`。

一個浮點數字面值（必須有小數點才可使用）可以加上以下後綴：

| 後綴 | 型別          |
| ---- | ------------- |
| `F`  | `float`       |
| `L`  | `long double` |

---

字元和字串字面值預設是 `char` 和 `const char[]` 型別，可以使用以下前綴（大小寫敏感）來改變型別（或陣列元素的型別）。

| 前綴 | 型別       |
| ---- | ---------- |
| `L`  | `wchar_t`  |
| `u8` | `char8_t`  |
| `u`  | `char16_t` |
| `U`  | `char32_t` |

其中 `u8` 只有字串字面值可以使用。

字元字面值以單引號包裹，字串字面值以雙引號包裹，其中可以使用跳脫序列（escape sequence）來表示特殊字元。

| 跳脫序列     | 字元                       |
| ------------ | -------------------------- |
| `\'`         | 單引號（single quote）     |
| `\"`         | 雙引號（double quote）     |
| `\?`         | 問號（question mark）      |
| `\\`         | 反斜線（backslash）        |
| `\a`         | 響鈴（audible bell）       |
| `\b`         | 退格（backspace）          |
| `\f`         | 換頁（form feed）          |
| `\n`         | 換行（line feed）          |
| `\r`         | 回車（carriage return）    |
| `\t`         | 水平製表（horizontal tab） |
| `\v`         | 垂直製表（vertical tab）   |
| `\000`       | 位元組 `000`，八進位表示   |
| `\x00`       | 位元組 `00`，十六進位表示  |
| `\u0000`     | Unicode 碼點 `U+0000`      |
| `\U00000000` | Unicode 碼點 `U+00000000`  |

前綴 `R` 可以關閉跳脫序列，詳細用法見 [cppreference](https://zh.cppreference.com/mwiki/index.php?title=cpp/language/string_literal&variant=zh-tw)。

一個字串字面值的陣列長度和看起來不會一樣，例如 `"C++"` 的長度為 4，因為其結尾會有一個空字元 `\0`，這是 C 式字串的特性：空結尾（null-terminated）。

## 標準輸出與標準輸入

先前說過，`iostream` 中提供了輸出、輸入相關的操作介面，這一節將說明更多應用。

### 輸出

`<<` 運算子會輸出右運算元，然後回傳輸出流，因此可以連續使用。
且其能輸出各種型別的物件，包含整數、浮點數、字元、指標（會輸出記憶體位址）等。

<pre>
<code><span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token string">"Hello "</span> &lt;&lt; <span class="token number">20</span>;
</code></pre>

等等，陣列會被隱式轉換成指標，那我們是怎麼輸出字串的？
之前提過，C 式字串實際上是字元陣列，並且以空字元結尾，因此我們只需要輸出 `*(ptr + idx)`，直到空字元即可。

標準庫還提供了一些方法來控制輸出的行為：

`std::flush`
: 刷新輸出流，也就是把緩衝區（buffer）中的字元輸出。

`std::endl`
: 插入換行並刷新流。

`std::setprecision`
: 設定數值精度。
  當數值無法在指定位數內表示，將使用科學記號。
  
  <pre>
  <span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">setprecision</span>(<span class="token number">3</span>) &lt;&lt; <span class="token number">3.1415</span>; <span class="token comment">// 輸出 `3.14`。</span>
  </code></pre>

`std::fixed`
: 設定小數位數。
  
  <pre>
  <code><span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">fixed</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">setprecision</span>(<span class="token number">3</span>) &lt;&lt; <span class="token number">3.00014</span>; <span class="token comment">// 輸出 `3.000`。</span>
  </code></pre>

`std::setw`、`std::setfill`、`std::left`、`std::right`
: <pre>
  <code><span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">setw</span>(<span class="token number">10</span>)     <span class="token comment">// 設定寬度。</span>
            &lt;&lt; <span class="token namespace">std</span>::<span class="token function">setfill</span>(<span class="token char">' '</span>) <span class="token comment">// 設定填充字元。</span>
            &lt;&lt; <span class="token namespace">std</span>::<span class="token function">right</span>        <span class="token comment">// 靠右對齊。</span>
            &lt;&lt; <span class="token number">3.1415</span>;           <span class="token comment">// 輸出 `    3.1415`。</span>
  </code></pre>

### 輸入

標準輸入流 `std::cin` 和 `std::cout` 相似，可以使用 `>>` 來「流入」。

<pre>
<code><span class="token keyword">int</span> input;
<span class="token namespace">std</span>::<span class="token gvariable">cin</span> &gt;&gt; input;
</code></pre>

## 實作猜數字遊戲

利用先前的知識，可以寫出以下的程式：

<pre>
<code><div class="wrapper">
<div class="gutter linenumber"><span data-linenumber="1"></span>
<span data-linenumber="2"></span>
<span data-linenumber="3"></span>
<span data-linenumber="4"></span>
<span data-linenumber="5"></span>
<span data-linenumber="6"></span>
<span data-linenumber="7"></span>
<span data-linenumber="8"></span>
<span data-linenumber="9"></span>
<span data-linenumber="10"></span>
<span data-linenumber="11"></span>
</div>
<div class="code"><span class="token keyword">#include</span> <span class="token string">&lt;iostream&gt;</span>

<span class="token keyword">int</span> <span class="token function">main</span>() {
    <span class="token keyword">int</span> answer = <span class="token number">5</span>;
    <span class="token keyword">int</span> input;

    <span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token string">"輸入一個 1~10 的整數。"</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">endl</span>;
    <span class="token namespace">std</span>::<span class="token gvariable">cin</span> &gt;&gt; input;

    <span class="token keyword">return</span> <span class="token number">0</span>;
}
</div></div></code></pre>

要判斷輸入的數字是否正確可以使用 `if`，在後方放一對括號，其中放入條件（一個布林值），就可以做到「如果（if）條件成立，才做某件事」。
可以再加上 `else`，當條件不成立時做另一件事。

因此我們在程式碼中加上：

<pre>
<code><div class="wrapper">
<div class="gutter linenumber"><span data-linenumber="10"></span>
<span data-linenumber="11"></span>
<span data-linenumber="12"></span>
<span data-linenumber="13"></span>
<span data-linenumber="14"></span>
</div>
<div class="code">    <span class="token keyword">if</span> (input == answer) {
        <span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token string">"猜對了！"</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">endl</span>;
    } <span class="token keyword">else</span> {
        <span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token string">"猜錯了！正確答案是："</span> &lt;&lt; answer << <span class="token namespace">std</span>::<span class="token function">endl</span>;
    }
</div></div></code></pre>

其中 `==` 是等於運算子（equal-to operator），會在兩邊的運算元相等時回傳 `true`，否則回傳 `false`。

不過現在每次的答案都是 5，很無聊，要隨機產生答案才行。
因此引入 `cstdlib`，並將字面值 `5` 改成 `std::rand() % 10 + 1`。
`%` 是取餘運算子（remainder operator），將亂數除以 10 的餘數加上 1，得到的結果便必定落在 1 到 10 之間。

不過這樣每次產生的亂數都一樣，這是因為電腦只能通過數學計算取得偽亂數（pseudo random），只要種子一樣就會產生一樣的偽亂數序列，這也是為什麼在 Minecraft 中同樣種子會生成一樣的「隨機」世界。
要修正這個問題，要引入 `ctime`，並在呼叫 `std::rand` 前使用 `std::srand(std::time(nullptr))` 將時間設為種子。

最終程式碼：

<pre>
<code><div class="wrapper">
<div class="gutter linenumber"><span data-linenumber="1"></span>
<span data-linenumber="2"></span>
<span data-linenumber="3"></span>
<span data-linenumber="4"></span>
<span data-linenumber="5"></span>
<span data-linenumber="6"></span>
<span data-linenumber="7"></span>
<span data-linenumber="8"></span>
<span data-linenumber="9"></span>
<span data-linenumber="10"></span>
<span data-linenumber="11"></span>
<span data-linenumber="12"></span>
<span data-linenumber="13"></span>
<span data-linenumber="14"></span>
<span data-linenumber="15"></span>
<span data-linenumber="16"></span>
<span data-linenumber="17"></span>
<span data-linenumber="18"></span>
<span data-linenumber="19"></span>
<span data-linenumber="20"></span>
<span data-linenumber="21"></span>
</div>
<div class="code"><span class="token keyword">#include</span> <span class="token string">&lt;iostream&gt;</span>
<span class="token keyword">#include</span> <span class="token string">&lt;cstdlib&gt;</span>
<span class="token keyword">#include</span> <span class="token string">&lt;ctime&gt;</span>

<span class="token keyword">int</span> <span class="token function">main</span>() {
    <span class="token namespace">std</span>::<span class="token function">srand</span>(<span class="token namespace">std</span>::<span class="token function">time</span>(<span class="token keyword">nullptr</span>));

    <span class="token keyword">int</span> answer = <span class="token namespace">std</span>::<span class="token function">rand</span>() % <span class="token number">10</span> + <span class="token number">1</span>;
    <span class="token keyword">int</span> input;

    <span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token string">"輸入一個 1~10 的整數。"</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">endl</span>;
    <span class="token namespace">std</span>::<span class="token gvariable">cin</span> &gt;&gt; input;

    <span class="token keyword">if</span> (input == answer) {
        <span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token string">"猜對了！"</span> &lt;&lt; <span class="token namespace">std</span>::<span class="token function">endl</span>;
    } <span class="token keyword">else</span> {
        <span class="token namespace">std</span>::<span class="token gvariable">cout</span> &lt;&lt; <span class="token string">"猜錯了！正確答案是："</span> &lt;&lt; answer << <span class="token namespace">std</span>::<span class="token function">endl</span>;
    }

    <span class="token keyword">return</span> <span class="token number">0</span>;
}
</div></div></code></pre>

注意這並不是最佳實作，此程式碼只是作為示例。

# 前置處理器

前置處理器指令會在編譯之前執行，替換掉原始碼的一些內容，並且永遠以井號開頭、換行結尾。

## 引入

我們已經看過 `#include` 指令很多次了，它可以找到指定的檔案，並把內容複製到你的程式碼中。
當引數是以角括號包裹時，前置處理器會從系統目錄和編譯時指定的目錄找，使用雙引號則是從當前目錄，更詳細的說明請見 [cppreference](https://zh.cppreference.com/mwiki/index.php?title=cpp/preprocessor/include&variant=zh-tw)。

因此，通常我們需要把 `#include` 放在檔案的開頭，否則，因為 C\+\+ 編譯器是由上到下讀取，在 `#include` 之前的程式碼將無法使用之後才引入的東西。

### 標頭檔

標頭檔（header files），也就是被引入的檔案，應該要能夠單獨編譯，也就是說其內容應該是完整的 C\+\+ 程式碼。
如果單純要插入內容，建議使用副檔名 `.inc`。

## 定義

使用 `#define` 定義的東西稱作巨集（macro），會在編譯之前被展開，也就是取代成原本的內容。為了方便辨識，巨集會使用全部大寫，並以底線分隔字詞。

<pre>
<code><span class="token keyword">#define</span> <span class="token macro">PI</span> (<span class="token number">3.1415F</span>)
</code></pre>

注意這並不是一個變數，`PI` 不會佔用記憶體，而是在編譯之前，所有的 `PI` 都會被取代成 `(3.1415F)`。
數字加上括號是為了避免在某些地方被展開導致非預期的結果。

---

巨集也可以接受引數：

<pre>
<code><span class="token keyword">#define</span> <span class="token macro">MAX(a, b)</span> (a > b ? a : b)
</code></pre>

其中 `? :` 是條件運算子（conditional operator），也是 C\+\+ 中唯一一個接受三個運算元的運算子，因此也有人直接將其稱作三元運算子。
當第一個運算元為 `true`，會回傳第二個運算元，反之回傳第三個。

## 條件編譯

所謂條件編譯，顧名思義，只在某些情況下編譯某些程式碼。

### 引入防範

由於 `#include` 指令只是複製貼上，因此如果引入同一個標頭檔兩次，便會因為重複定義造成錯誤，或造成編譯時間延長。
對於這個問題，最常見的做法是使用引入防範（include guard），這也是條件編譯最常見的使用情境。

<pre>
<code><span class="token keyword">#ifndef</span> <span class="token macro">CPPTUTORIAL_EXAMPLE_HEADER_H</span> <span class="token comment">// 如果沒有定義……</span>
<span class="token keyword">#define</span> <span class="token macro">CPPTUTORIAL_EXAMPLE_HEADER_H</span>

<span class="token comment">// 內容。</span>

<span class="token keyword">#endif</span>
</code></pre>

引入防範的巨集名稱應盡可能獨一無二，通常使用專案名稱和標頭檔路徑。

另一種做法是在標頭檔的第一行使用非標準的指令 `#pragma once`，如果編譯器不支援會直接忽略，因此不建議使用。

---

版權所有 (c) 2022 Luminous-Coder  
所有內容在 [CC「姓名標示—非商業性—同方式分享」4.0 國際公眾授權條款](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.zh-Hant) 下發佈。

<a href='https://ko-fi.com/luminouscoder' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi1.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

{%hackmd @Luminous-Coder/dark-theme %}

[^CLion]: CLion 需要付費，但如果你是學生便可以申請教育方案，免費使用 JetBrains 的各種 IDE，GitHub Student Developer Pack 中也有贈送。
但也請注意 CLion 的一些功能或許會造成初學者的困惑。
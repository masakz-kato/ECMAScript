# JavaScriptの特徴

- ケースセンシティブ（大文字と小文字を区別）
- Unicode


#文法
命令は文 (statement) と呼ばれ、セミコロン (;) によって区切られる。
行の終わりにセミコロンを自動で挿入するルール (ASI) があるが、
副作用を防ぐため、常に文の終わりにはセミコロンを入れる事。

## コメント

```javascript
// 一行のコメント

/* 複数行
　　コメント
 */

/* ただし、コメントは /* ネストできません */ SyntaxError */
```

## strictモード（厳格モード）
strictモードとは、通常の JavaScript 従来は受け入れていた一部のミスをエラーに変更します。これにより開発者はよりエラーに気づきやすくなります。

### 使い方
“use strict”; (または ‘use strict’;) という文をそのまま追加します。
strict モードはスクリプト全体または個別の関数に適用できます。

**スクリプト全体に適応**
```javascript
'use strict';
var x = 1;
```
> **注意**
> 連結すると全てがstrictモードになる。
> ```javascript
> //strict.js
> 'use strict';
> function strict() {
>   var message = "this function is Strict Mode!";
>   return message;
> }
> require('./notStrict.js')
> ```
> ```javascript
> //notStrict.js
> function noStrict() {
>   var message = "this function is Not Strict Mode!";
>   return message;
> }
> ```


<details>
<summary>全体適応する場合の注意</summary>**連結すると全てがstrictになる。**
<div>```javascript:sample.js
puts 'Hello, World'
```
</div>
</details>

**関数内のスコープのみに適応**
```javascript
//この関数はstrictモードで動作
function strict() {
    "use strict";

    var message = "this function is Strict Mode!";
    return message;
}

//この関数は非strictモードで動作
function noStrict() {
    var message = "this function is Not Strict Mode!";
    return message;
}

//“use strict”宣言は、関数スコープにつき1つのみ
function outer() {
    "use strict";

    function inner() {
        "use strict";  //ERROR: Unnecessary 'use strict'.

        window.console.log("hoge");
    }

    inner();
}
```

非strict のスクリプトと strictのスクリプトを連結すると非strict になります。

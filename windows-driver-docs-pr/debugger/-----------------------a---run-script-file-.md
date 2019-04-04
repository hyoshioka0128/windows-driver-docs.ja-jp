---
title: $、$、$、$、$$ (スクリプトの実行ファイル)
description: $、$、$$ $$、および $$、コマンドは、指定したスクリプト ファイルの内容を読み取るし、デバッガー コマンドの入力としてその内容を使用します。
ms.assetid: b3584680-765d-4aaf-ad43-c7d73552e5fb
keywords:
- $ (スクリプト ファイルを実行) コマンド
- $ (スクリプト ファイルを実行) コマンド
- $ (スクリプト ファイルを実行) コマンド
- スクリプト ファイル ($) のコマンドを実行します。
- スクリプト ファイル ($) のコマンドを実行します。
- スクリプト ファイル ($$) のコマンドを実行します。
- スクリプト ファイル ($$) の通信を実行します。
- $、$、$、$、$$ デバッグ (スクリプトの実行ファイル) の Windows
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $ , $ , $$ , $$ , $$ a (Run Script File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b6d169b34905526d7358f1dbe4c93883935a991
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572939"
---
# <a name="-----a-run-script-file"></a>$<、$><、$$<、$$><、$$ >a< (スクリプト ファイルの実行)


**$ &lt;**、 **$ &gt; &lt;**、 **$$ &lt;**、 **$$ &gt; &lt;** 、および**$$ &gt;、&lt;** コマンド ファイルを開きとしてその内容を使用して、指定したスクリプトの内容を読み取るデバッガーのコマンドを入力します。

```dbgcmd
    $<Filename 
    $><Filename 
    $$<Filename 
    $$><Filename 
    $$>a<Filename [arg1 arg2 arg3 ...] 
```

## <a name="span-idddkcmdrunscriptfiledbgspanspan-idddkcmdrunscriptfiledbgspanparameters"></a><span id="ddk_cmd_run_script_file_dbg"></span><span id="DDK_CMD_RUN_SCRIPT_FILE_DBG"></span>パラメーター


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *ファイル名*   
有効なデバッガー コマンド テキストを含むファイルを指定します。 ファイル名は、Microsoft Windows ファイル名前付け規則に従う必要があります。 ファイル名には、スペースを含めることがあります。

<span id="_______argn______"></span><span id="_______ARGN______"></span> *argn*   
デバッガーをスクリプトに渡す引数を文字列の任意の数を指定します。 デバッガーは、$ の任意の文字列に置き換わります {$arg*n*} で対応するスクリプト ファイルで*argn*スクリプトを実行する前にします。 引数には引用符またはセミコロンを含めることはできません。 複数の引数をスペースで区切る必要があります。引数にスペースが含まれている場合は、引用符で囲む必要があります。 すべての引数は省略可能です。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**$$ &lt;** と**$ &lt;** トークンは、文字どおり、スクリプト ファイルに含まれるコマンドを実行します。 ただし、 **$ &lt;** セミコロンを含む 1 つ以上の任意のファイル名を指定することができます。 **$ &lt;** により、ファイル名に使用するのにはセミコロンを連結することはできません**$ &lt;** を他のデバッガー コマンドでは、ため、コマンドの区切り記号およびファイル名の一部として、セミコロンを使用できません。

**$$ &gt; &lt;** と**$ &gt; &lt;** トークンは、文字どおり、スクリプト ファイルに含まれるコマンドを実行します。つまり、スクリプト ファイルを開き、セミコロンでは、すべての改行を置き換えますおよび 1 つのコマンド ブロックとして生成されるテキストを実行します。 同様**$ &lt;** 、先ほど説明した、 **$ &gt; &lt;** バリエーションにより、セミコロンを含むファイル名、つまり連結することはできません**$ &gt; &lt;** 他のデバッガー コマンドを使用します。

**$$ &gt; &lt;** と**$ &gt; &lt;** トークンは、デバッガー コマンドが含まれているスクリプトを実行している場合に役立ちます。プログラム。 これらのプログラムの詳細については、[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)を参照してください。

セミコロンを含むファイル名がない場合はいずれかを使用する必要はありません**$ &lt;** または **$ &gt; &lt;** します。

**$$ &gt;、&lt;** トークンを使用すると、デバッガーは、スクリプトに引数を渡します。 場合*Filename*スペースが含まれることは、引用符で囲む必要があります。 引数が多すぎますが指定されている場合は、余分な引数は無視されます。 フォーム $ のソース ファイルでトークンのいずれかの引数が少なすぎますを指定した場合 {$arg*n*} ここ*n*は指定された引数の数のリテラル形式のままになりますでは置き換えられませんよりも大きくなります。何か。 このコマンドをセミコロンでおよびその他のコマンドを利用できます。セミコロンの有無は、引数リストを終了します。

コマンドとその出力が表示される、デバッガーは、スクリプト ファイルを実行するとき、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 スクリプト ファイルの末尾に達すると、デバッガーに制御が戻ります。

次の表では、これらのトークンを使用する方法を示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Token</th>
<th align="left">セミコロンが含まれているファイル名を使用できます。</th>
<th align="left">セミコロンで区切られた追加のコマンドの連結を許可します。</th>
<th align="left">は、1 つのコマンド ブロックをまとめます</th>
<th align="left">スクリプトの引数は、します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$&lt;</strong></p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$&gt;&lt;</strong></p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$$&lt;</strong></p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$$&gt;&lt;</strong></p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$$&gt;A&lt;</strong></p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>はい</p></td>
</tr>
</tbody>
</table>

 

**$ &lt;**、 **$ &gt; &lt;**、 **$$ &lt;**、および**$$ &gt; &lt;** コマンド エコー スクリプトに含まれるコマンドは、ファイルし、これらのコマンドの出力を表示します。 **$$ &gt;、&lt;** コマンドは、スクリプト ファイルのあるコマンドはエコーしませんが、単に出力が表示されます。

スクリプト ファイルは、入れ子にすることができます。 デバッガーには、スクリプト ファイルでこれらのトークンのいずれかが発生すると、実行は、新しいスクリプト ファイルに移動し、前の場所に新しいスクリプト ファイルが完了したときに返されます。 スクリプトは、再帰的に呼び出すことができます。

、WinDbg では、デバッガー コマンド ウィンドウで、追加のコマンド テキストを貼り付けることができます。

<a name="examples"></a>使用例
--------

次の例では、スクリプト ファイル、Myfile.txt に引数を渡す方法を示します。 ファイルに次のテキストが含まれていると仮定します。

```console
.echo The first argument is ${$arg1}.
.echo The second argument is ${$arg2}.
```

このようなコマンドを使用してこのファイルに引数を渡すことができます。

```console
0:000> $$>a<myfile.txt myFirstArg mySecondArg 
```

このコマンドの結果は次のようになります。

```console
The first argument is myFirstArg.
The second argument is mySecondArg.
```

間違った数の引数が指定されている場合の動作の例を次に示します。 マイ Script.txt ファイルに次のテキストが含まれていると仮定します。

```console
.echo The first argument is ${$arg1}.
.echo The fifth argument is ${$arg5}.
.echo The fourth argument is ${$arg4}.
```

次のセミコロンで区切られたコマンド ラインは出力したがってされます。

```console
0:000> $$>a< "c:\binl\my script.txt" "First one" Two "Three More" Four; recx 
The first argument is First one.
The fifth argument is ${$arg5}.
The fourth argument is Four.
ecx=0021f4ac
```

前の例では、スペースが含まれているし、も引用符で囲まれた空白文字を含む引数であるために、ファイル名は引用符で囲みます。 セミコロンが終了しますが、5 番目の引数は、スクリプトが期待される動作ですが、 **$$ &gt;、&lt;** 4 番目の引数の後にコマンド。

 



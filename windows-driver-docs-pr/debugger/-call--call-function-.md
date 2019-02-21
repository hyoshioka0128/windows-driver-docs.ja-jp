---
title: .call (関数の呼び出し)
description: .Call コマンドでは、関数を実行するターゲット プロセスを実行します。
ms.assetid: 93265c2a-ea4d-4523-928c-1bb75a9356b1
keywords:
- .call (関数の呼び出し) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .call (Call Function)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a4d7edfab7998d62d2696b5d351264cbfeb37f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530087"
---
# <a name="call-call-function"></a>.call (関数の呼び出し)


**.Call**コマンドは、関数を実行するターゲット プロセスを実行します。

```dbgsyntax
.call [/v] Function( Arguments ) 
.call /s Prototype Function( Arguments ) 
.call /c 
.call /C 
```

## <a name="span-idddkmetacallfunctiondbgspanspan-idddkmetacallfunctiondbgspanparameters"></a><span id="ddk_meta_call_function_dbg"></span><span id="DDK_META_CALL_FUNCTION_DBG"></span>パラメーター


<span id="________v______"></span><span id="________V______"></span> **/v**   
呼び出しとその引数の詳細情報が表示されます。

<span id="________s________Prototype______"></span><span id="________s________prototype______"></span><span id="________S________PROTOTYPE______"></span> **/s** *プロトタイプ*   
指定されている関数を呼び出すことができます*関数*場合でも、適切なシンボルがあるありません。 この場合、別の関数を呼び出すしようとする関数と同じ呼び出しのプロトタイプを持つ記号が必要です。 *プロトタイプ*パラメーターは、このプロトタイプ関数の名前。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span> *関数*   
呼び出される関数を指定します。 (可能であればで修飾モジュール名)、関数または他の関数のアドレスに評価される式の名前を指定できます。 コンス トラクターまたはデストラクターを呼び出す必要がある場合する必要があります--アドレス指定を使用してください、C++ 式の演算子の名前付きの構文を評価する (を参照してください[数値式の構文](numerical-expression-syntax.md)詳細については)。

<span id="_______Arguments______"></span><span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> *引数*   
関数に渡される引数を指定します。 メソッドを呼び出す場合、最初の引数がある必要があります**この**、他のすべての引数が続くとします。 引数は、コンマで区切る必要があり、通常の引数の構文に一致する必要があります。 可変長引数リストがサポートされています。 引数内の式は C++ の式エバリュエーターで解析され参照してください[C++ 数字と演算子](c---numbers-and-operators.md)詳細についてはします。 引数としてリテラル文字列を入力することはできませんが、文字列、またはターゲット プロセスにアクセス可能な他の任意のメモリへのポインターを使用することができます。

<span id="________c______"></span><span id="________C______"></span> **/c**   
現在のスレッドで、既存の呼び出しをクリアします。

<span id="________C______"></span><span id="________c______"></span> **/C**   
現在のスレッドで、既存の呼び出しをクリアし、未処理の呼び出しによって格納されるコンテキストに、現在のスレッドのコンテキストをリセットします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>x86 と x64 のみ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

指定された関数は、現在のプロセスの現在のスレッドによって呼び出されます。

のみ、 **cdecl**、 **stdcall**、 **fastcall**、および**thiscall**呼び出し規約がサポートされています。 このコマンドでは、マネージ コードを呼び出すことができません。

後 **.call**が使用すると、デバッガーは、スタックを更新、呼び出された関数の先頭をポイントし、停止を命令ポインターを変更します。 使用[ **g (移動)** ](g--go-.md) 、実行を再開または **~. g**呼び出しを行っているスレッドだけを実行します。

関数から制御が戻るときに中断が生じるし、デバッガーには、関数の戻り値が表示されます。 戻り値が格納されていることも、 **$callret**擬似レジスタは、戻り値の型を取得します。

CTRL キーを押しながら C キーまたは CTRL + BREAK を使用してターゲットが破損した場合、現在のスレッドは、侵入を処理するために作成された追加のスレッドにします。 発行した場合、 **.call**余分なスレッドは、呼び出された関数の使用はこの時点では、コマンドします。

定義済みのブレークポイントに到達した場合、余分な侵入のスレッドがありません。 使用する場合 **.call**使用することがユーザー モードでのブレークポイントをしながら[ **g** ](g--go-.md)全体のプロセスを実行するまたは **~. g**を実行するだけで現在のスレッド。 使用して**g** 1 つのスレッドを実行し、この新しい関数を迂回することがあるために、プログラムの動作を損なう可能性があります。 その一方で、このスレッドがまだロックと、他の属性と、それに伴って **~. g**リスク デッドロックの可能性があります。

使用する最も安全な方法 **.call**特定の関数を安全に呼び出すことがいる場所に、コードでブレークポイントを設定します。 使用することがそのブレークポイントがヒットしたら、 **.call**を実行するには、その関数を希望する場合。 使用する場合 **.call**ポイントでは、この関数呼び出すことは通常できません、デッドロックまたはターゲットの破損がなる可能性があります。

既存のコードによって呼び出されることはありませんが、デバッガーによって呼び出されるものは、ソース コードを追加の関数を追加すると便利かもしれません。 たとえば、コードとその環境の現在の状態を調査し、既知のメモリ位置に、状態に関する情報を格納に使用される関数を追加できます。 コードを最適化しないようにしてくださいまたはコンパイラによってこれらの関数を削除する可能性があります。 最後の手段としてのみため、この手法を使用して、アプリケーションがクラッシュした場合 **.call**ダンプ ファイルをデバッグするときに使用できませんがします。

**.Call/c**と **.call/C**コマンドを使用した場合にのみ使用する必要があります **.call**が失敗したに入る前に頭を変更した場合や、 [ **g** ](g--go-.md)コマンド。 これらは適していない決然、破損している対象の状態につながる未完了の呼び出しを破棄するためです。

次のコード例に示す方法、 **.call/s**コマンドを使用します。

```dbgcmd
.call /s KnownFunction UnknownFunction( 1 )
```

この例でのプライベート シンボルがある**KnownFunction**は整数を受け取ってとしてその唯一の引数と戻り値は、たとえば、配列へのポインター。 シンボルがないか、または可能性があるだけであるパブリック シンボルを**UnknownFunction**、唯一の引数として整数を受け取るし、配列へのポインターを返しますがわかっています。 使用して、 **/s**オプション、ことを指定できる**UnknownFunction**と、同じ動作方法**KnownFunction**は。 呼び出しを正常に生成するために、 **UnknownFunction**します。

 

 






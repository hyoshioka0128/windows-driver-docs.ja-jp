---
title: .f+、.f- (ローカル コンテキストのシフト)
description: .F + コマンドは、現在のスタック内の次のフレームにフレーム インデックスを移動します。 .F コマンドは、現在のスタック内の前のフレームにフレーム インデックスを移動します。
ms.assetid: aade5ec0-4d40-4ff1-9d4b-f3ad81b54b79
keywords:
- .f +、.f - (shift キーをローカル コンテキスト) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .f+, .f- (Shift Local Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7dff1469610c6659ceb2b7a1d9003cd93bfa07c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582197"
---
# <a name="f-f--shift-local-context"></a>.f+、.f- (ローカル コンテキストのシフト)


**.F +** コマンドでは、現在のスタック内の次のフレームにフレーム インデックスを移動します。 **.F-** コマンドでは、現在のスタック内の前のフレームにフレーム インデックスを移動します。

```dbgcmd
.f+  
.f-  
```

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ローカル コンテキストとその他のコンテキストの設定の詳細については、[変更コンテキスト](changing-contexts.md)を参照してください。 ローカル変数とその他のメモリに関連するコマンドを表示する方法の詳細については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>コメント
-------

*フレーム*デバッガーはローカル変数の解釈を使用してローカル コンテキスト (スコープ) を指定します

**.F +** .f コマンドは、現在のスタック内の次または前のフレームに移動するためのショートカットとします。 これらのコマンドは、次に相当[ **.frame** ](-frame--set-local-context-.md)コマンドが、 **.f**コマンドは、利便性のために短くなります。

-   **.f +** と同じ **.frame @$ フレームは + 1**します。

-   **.f -** と同じ **.frame @$ フレーム - 1**します。

ドル記号 ($) の識別、フレームの値として、[擬似レジスタ](pseudo-register-syntax.md)します。 アット マーク (@ により、デバッガーに値をより迅速にアクセスする文字列が登録または擬似レジスタである、デバッガーに通知されるためです。

アプリケーションが実行されているときに、ローカル変数の意味で定義されている関数にのみこのような変数のスコープを拡張するため、プログラム カウンターの場所に依存します。 使用しない限り、 **.f +** または **.f -** コマンド (または[ **.frame** ](-frame--set-local-context-.md)コマンド)、デバッガーは、現在の関数 (現在のスコープを使用します。スタックのフレーム) ローカル コンテキストとします。

*フレーム番号*はスタック トレース内でスタック フレームの位置です。 このスタック トレースを表示するにを使用して、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドまたは[コール スタック ウィンドウ](calls-window.md)します。 最初の行 (現在のフレーム) では、フレーム番号は 0 を表します。 それ以降の行は、フレーム番号 1、2、3 を表し、具合です。

新しいローカル変数の情報を表示する別のスタック フレームには、ローカル コンテキストを設定できます。 ただし、使用できる実際の変数は、実行されるコードに依存します。

デバッガーでは、任意のプログラムの実行が発生した場合に、プログラム カウンターのスコープに、ローカル コンテキストをリセットします。 ローカル コンテキストは、レジスタのコンテキストが変更された場合、最上位のスタック フレームにリセットされます。

 

 






---
title: dv (ローカル変数の表示)
description: Dv コマンドは、現在のスコープの名前とすべてのローカル変数の値を表示します。
ms.assetid: 1b5260f7-f47c-481a-b93f-015ab9fa4b58
keywords:
- dv (ローカル変数の表示) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dv (Display Local Variables)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b4e17826565a066df5572d392a32008929e9169
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538613"
---
# <a name="dv-display-local-variables"></a>dv (ローカル変数の表示)


**Dv**コマンドが現在のスコープ内の名前とすべてのローカル変数の値を表示します。

```dbgcmd
dv [Flags] [Pattern] 
```

## <a name="span-idddkcmddisplaylocalvariablesdbgspanspan-idddkcmddisplaylocalvariablesdbgspanparameters"></a><span id="ddk_cmd_display_local_variables_dbg"></span><span id="DDK_CMD_DISPLAY_LOCAL_VARIABLES_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
追加情報が表示されます。 大文字の次のいずれか*フラグ*含めることができます。

<span id="_f__addr_"></span><span id="_F__ADDR_"></span>**/f** &lt;addr&gt;  
任意のコードを任意の場所のどのようなパラメーターとローカル変数が存在できますが表示されるように、任意の関数のアドレスを指定できます。 値の表示をオフにし、意味 **/V**します。 **/F**フラグは、最後のフラグである必要があります。 パラメーター フィルター パターン文字列が引用符で囲まれた場合は、その後に指定できます。

<span id="_i"></span><span id="_I"></span>**/i**  
変数の種類を指定する表示: ローカル、グローバル、パラメーター、関数、または不明です。

<span id="_t"></span><span id="_T"></span>**/t**  
各ローカル変数のデータ型を含める表示をによりします。

<span id="_v"></span><span id="_V"></span>**/v**  
仮想メモリ アドレスを含めるか、各ローカル変数の場所を登録するためにディスプレイをによりします。

<span id="_V"></span><span id="_v"></span>**/V**  
同じ **/v**、関連する登録の基準としたローカル変数のアドレスも含まれています。

<span id="_a"></span><span id="_A"></span>**/a**  
出力をアドレス、昇順で並べ替えます。

<span id="_A"></span><span id="_a"></span>**/A**  
出力をアドレス、降順で並べ替えます。

<span id="_n"></span><span id="_N"></span>**/n**  
出力を昇順での名前で並べ替えます。

<span id="_N"></span><span id="_n"></span>**/N**  
出力を降順での名前で並べ替えます。

<span id="_z"></span><span id="_Z"></span>**/z**  
出力は、サイズの昇順で並べ替えます。

<span id="_Z"></span><span id="_z"></span>**/Z**  
出力は、サイズの降順で並べ替えます。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
により、コマンドは、指定された一致するローカル変数のみを表示する*パターン*します。 パターンは、さまざまなワイルドカードと指定子を含めることができます。参照してください[文字列のワイルドカード構文](string-wildcard-syntax.md)詳細についてはします。 場合*パターン*スペースが含まれることは、引用符で囲む必要があります。 場合*パターン*は省略すると、すべてのローカル変数が表示されます。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細の表示と変更のローカル変数とその他のメモリに関連するコマンドの説明については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>注釈
-------

詳細モードでは、変数のアドレスはも表示されます。 (でこれに行うこともできます、 [ **(シンボルを調べる) x** ](x--examine-symbols-.md)コマンド)。

データの構造体および未知のデータ型は、完全; には表示されません。代わりに、その型名が表示されます。 全体の構造を表示または構造体の特定のメンバーを表示を使用して、 [ **dt (型の表示)** ](dt--display-type-.md)コマンド。

*ローカル コンテキスト*決定ローカル変数のセットが表示されます。 既定では、このコンテキストは、プログラムのカウンターの現在の位置と一致します。 これを変更する方法については、[ローカル コンテキスト](changing-contexts.md#local-context)を参照してください。

 

 






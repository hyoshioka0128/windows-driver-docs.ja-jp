---
title: for_each_local
description: For_each_local 拡張機能は、現在のフレームでそれぞれのローカル変数に 1 回のデバッガー コマンドを実行します。
ms.assetid: 2b1d65e6-6322-404e-a94b-90a46035fe9e
keywords:
- Windows デバッグ for_each_local
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_local
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0272d43871bccc209522d4521113c2f2a1a31791
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336692"
---
# <a name="foreachlocal"></a>! の\_各\_ローカル


**! の\_各\_ローカル**拡張機能は、現在のフレームでデバッガー コマンドにそれぞれのローカル変数に 1 回を実行します。

```dbgcmd
!for_each_local ["CommandString"] 
!for_each_local -? 
```

## <a name="span-idddkforeachlocaldbgspanspan-idddkforeachlocaldbgspanparameters"></a><span id="ddk__for_each_local_dbg"></span><span id="DDK__FOR_EACH_LOCAL_DBG"></span>パラメーター


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
現在のスタック フレームでローカル変数ごとに 1 回を実行するデバッガー コマンドを指定します。 場合*クラスヒント*複数のコマンドが含まれていますをセミコロンで区切るしで囲む必要があります*クラスヒント*引用符で囲んで指定します。 個々 のコマンドを複数のコマンドを含める場合*クラスヒント*引用符を含めることはできません。

内で*クラスヒント*、またはいずれかのスクリプトをコマンドでは、*クラスヒント*実行は、使用することができます、  **@\#ローカル**エイリアス。 このエイリアスは、ローカル変数の名前に置換されます。 この置換の前に発生します*クラスヒント*が実行される前に、その他の解析に発生します。 このエイリアスは大文字小文字が区別し、その前にスペースを追加し、エイリアスをかっこで囲む場合でも、その後スペースを追加する必要があります。 C++ 式の構文を使用する場合は、としては、このエイリアスを参照する必要があります **@ (@\#ローカル)** します。

このエイリアスへの呼び出しの有効期間中にのみ使用可能な **! の\_各\_ローカル**します。 このエイリアス擬似レジスタを固定名のエイリアスまたはという名前のユーザーのエイリアスを混同しないでください。

<span id="_______-_______"></span> **-?**   
この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細を表示し、ローカル変数とその他のメモリに関連するコマンドの説明を変更する方法については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>注釈
-------

任意の引数を指定しない場合、 **! の\_各\_ローカル**拡張機能は、ローカル変数を一覧表示されます。 ローカル変数の詳細については、使用、 [ **dv (ローカル変数の表示)** ](dv--display-local-variables-.md)コマンド。

表示には、行うたびに、拡張機能が呼び出されたときに、ローカル変数の合計数が含まれていますデバッガーの詳細な出力を有効にした場合を*クラスヒント*ローカル変数では、その変数およびのテキストに対して実行される*クラスヒント*がエコーされます。

 

 






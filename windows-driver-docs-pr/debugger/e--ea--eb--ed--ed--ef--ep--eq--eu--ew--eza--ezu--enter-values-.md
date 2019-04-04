---
title: 電子メール、ea、eb、ed、eD、ef、ep、eq、eu、新しい、eza (値を入力してください)
description: E のコマンドは、メモリに指定した値を入力します。このコマンドと混同しないで、~ E (スレッド固有のコマンド) 修飾子。
ms.assetid: d21b13ac-2268-4218-b562-4c466956b05d
keywords:
- 電子メール、ea、eb、ed、eD、ef、ep、eq、eu、新しい、eza (入力の値) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- e, ea, eb, ed, eD, ef, ep, eq, eu, ew, eza (Enter Values)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f6d3ea07a9370798d35c9099ac3837a7b917b23
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349535"
---
# <a name="e-ea-eb-ed-ed-ef-ep-eq-eu-ew-eza-enter-values"></a>電子メール、ea、eb、ed、eD、ef、ep、eq、eu、新しい、eza (値を入力してください)


**E\\*** 指定した値をメモリにコマンドを入力します。

このコマンドと混同しないで、 [ **~ E (スレッド固有のコマンド)** ](-e--thread-specific-command-.md)修飾子。

```dbgcmd
e{b|d|D|f|p|q|w} Address [Values] 
e{a|u|za|zu} Address "String" 
e Address [Values]
```

## <a name="span-idddkcmdentervaluesdbgspanspan-idddkcmdentervaluesdbgspanparameters"></a><span id="ddk_cmd_enter_values_dbg"></span><span id="DDK_CMD_ENTER_VALUES_DBG"></span>パラメーター


### <a name="span-idsyntaxedefspanspan-idsyntaxedefspansyntax-ed-ef"></a><span id="syntax__ed_ef"></span><span id="SYNTAX__ED_EF"></span>ED ef の構文

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
開始アドレスの値を入力する場所を指定します。 デバッガーでの値と置き換えられる*アドレス*と各以降のメモリの場所まですべて*値*が使用されています。

<span id="_______Values______"></span><span id="_______values______"></span><span id="_______VALUES______"></span> *値*   
メモリに入力する 1 つまたは複数の値を指定します。 複数の数値は、スペースで区切る必要があります。 任意の値を指定しない場合は、現在のアドレスとそのアドレスの値が表示されます、および入力を求められます。

<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *文字列*   
メモリに入力される文字列を指定します。 **Ea**と**eza**コマンドは、ASCII 文字列としてメモリにこれを書き込み、 **eu**と**ezu**コマンドとしてメモリに書き込みます、Unicode 文字列。 **Eza**と**ezu**コマンド記述ターミナル**NULL**、 **ea**と**eu**コマンドはありません。 *文字列*引用符で囲む必要があります。

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

その他のメモリに関連するコマンドの説明とメモリの操作の概要については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>コメント
-------

このコマンドは、次の形式で存在します。 2 番目の文字、 **ed**と**eD**コマンドは大文字小文字を区別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">以下に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>e</strong></p></td>
<td align="left"><p>これが最も最近使用したのと同じ形式でデータを入力<strong>e<em> </strong>コマンド。 (場合、最も最近<strong>e</em></strong>コマンドが<strong>ea</strong>、 <strong>eza</strong>、 <strong>eu</strong>、または<strong>ezu</strong>、最後のパラメーターになります<em>文字列</em>省略しない可能性があります)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ea</strong></p></td>
<td align="left"><p>ASCII の文字列 (NULL で終了していません)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eb</strong></p></td>
<td align="left"><p>バイト値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ed</strong></p></td>
<td align="left"><p>ダブル ワード値 (4 バイト)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eD</strong></p></td>
<td align="left"><p>倍精度浮動小数点数 (8 バイト)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ef</strong></p></td>
<td align="left"><p>単精度浮動小数点数 (4 バイト)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ep</strong></p></td>
<td align="left"><p>ポインターのサイズの値。 このコマンドは<strong>ed</strong>または<strong>eq</strong>かどうか、ターゲット コンピューターのプロセッサ アーキテクチャは 32 ビットまたは 64 ビット、それぞれ異なりますが、します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>eq</strong></p></td>
<td align="left"><p>クワドワード値 (8 バイト)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eu</strong></p></td>
<td align="left"><p>Unicode の文字列 (NULL で終了していません)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ew</strong></p></td>
<td align="left"><p>Word の値 (2 バイト)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>eza</strong></p></td>
<td align="left"><p>NULL で終わる ASCII 文字列です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ezu</strong></p></td>
<td align="left"><p>NULL で終わる Unicode 文字列。</p></td>
</tr>
</tbody>
</table>

 

数値の値は、現在の基数 (16、10、または 8) では数値として解釈されます。 既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。 既定の基数を指定することによってオーバーライドできます、 **0 x**プレフィックス (16 進数)、 **0n**プレフィックス (10 進数)、 **0t**プレフィックス (8 進数)、または**0y**プレフィックス (バイナリ)。

**注**  既定の基数は C++ の式が使用されているときに動作が異なります。 参照してください[を評価する式](evaluating-expressions.md)詳細についてはします。

 

バイト値を入力するときに、 **eb**コマンドを単一引用符を使用して文字を指定することができます。 複数の文字を含める場合は、各手順は、独自の引用符で囲む必要があります。 これにより、null 文字で終了しない、文字の文字列を入力することができます。 例:

```dbgcmd
eb 'h' 'e' 'l' 'l' 'o'
```

C スタイルのエスケープ文字 (など '\\0' または'\\n') 以下のコマンドで使用することはできません。

省略した場合、*値*パラメーター、入力を求められます。 アドレスとその現在の内容が表示されます、および**入力&gt;** プロンプトが表示されます。 次のいずれかを行うことができます。

-   値を入力して ENTER キーを押して、新しい値を入力します。

-   スペースに続けて、ENTER キーを押して、メモリの現在の値を保持します。

-   ENTER キーを押して、コマンドを終了します。

 

 






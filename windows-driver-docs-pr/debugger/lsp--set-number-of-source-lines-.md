---
title: lsp (ソース行数の設定)
description: Lsp コマンドでは、ステップ実行またはコードを実行または %.*ls と lsa コマンドを使用中に、ソース行の数が表示されるを制御します。
ms.assetid: 350933f1-5459-4ba2-9ca7-a42341cf95de
keywords:
- lsp (設定数のソース行) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lsp (Set Number of Source Lines)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3350405a16da2b9fb75e8f41f73ae1c48e902897
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383313"
---
# <a name="lsp-set-number-of-source-lines"></a>lsp (ソース行数の設定)


**Lsp**コマンドは、ステップ実行中に表示されるソース行の数、またはコードを実行したりを使用して、制御、 [ **ls および lsa コマンド**](ls--lsa--list-source-lines-.md)します。

```dbgcmd
lsp [-a] LeadingLines TrailingLines 
lsp [-a] TotalLines 
lsp [-a] 
```

## <a name="span-idddkcmdsetnumberofsourcelinesdbgspanspan-idddkcmdsetnumberofsourcelinesdbgspanparameters"></a><span id="ddk_cmd_set_number_of_source_lines_dbg"></span><span id="DDK_CMD_SET_NUMBER_OF_SOURCE_LINES_DBG"></span>パラメーター


<span id="_______-a______"></span><span id="_______-A______"></span> **-**    
設定または行の数を表示する **%.*ls**と**lsa**を表示します。 省略した場合 **-a**、 **lsp**をステップ実行し、コードを実行するときに示されている行の数を表示または設定します。

<span id="_______LeadingLines______"></span><span id="_______leadinglines______"></span><span id="_______LEADINGLINES______"></span> *LeadingLines*   
現在の行の前に表示する行の数を指定します。

<span id="_______TrailingLines______"></span><span id="_______trailinglines______"></span><span id="_______TRAILINGLINES______"></span> *TrailingLines*   
現在の行後を表示する行の数を指定します。

<span id="_______TotalLines______"></span><span id="_______totallines______"></span><span id="_______TOTALLINES______"></span> *TotalLines*   
表示する行の合計数を指定します。 この数は、先頭と末尾の行の間で均等に分割します。 (この数値が奇数の場合は、末尾行が表示されます。)

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

 

<a name="remarks"></a>注釈
-------

使用すると、 **lsp**コマンド、パラメーターのないと共に**lsp**現在の先頭行とステップ実行時に使用した後続の線の値が表示されます。 と共にのみ、このコマンドを使用すると、 **-a**パラメーター、 **lsp**ステップ実行中を使用した値が表示されます、 [ **ls および lsa コマンド**](ls--lsa--list-source-lines-.md).

プログラムをステップ実行か、後改ページするプログラムの実行、以前**lsp**コマンドは、先頭と末尾に表示される行の数を決定します。 使用すると**lsa**、前の**lsp-a**コマンドは、先頭と末尾に表示される行の数を決定します。 使用すると **%.*ls**、すべての行として表示される 1 つのブロックので、以前**lsp-a**コマンドが表示される行の合計数を決定します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソースのデバッグと関連するコマンドの詳細については、次を参照してください。[元のモードでデバッグ](debugging-in-source-mode.md)します。

 

 






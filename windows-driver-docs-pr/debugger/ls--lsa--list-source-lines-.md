---
title: ls、lsa (ソース行の一覧表示)
description: Ls および lsa コマンドは、一連の現在のソース ファイルから線を表示し、現在のソース行番号を進めます。
ms.assetid: ca5cd2f7-4920-4d36-b338-c934451bc511
keywords:
- ls、lsa (一覧のソース行) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ls, lsa (List Source Lines)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ff14372ab89b3458bacd43e782d87b23132d5cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383322"
---
# <a name="ls-lsa-list-source-lines"></a>ls、lsa (ソース行の一覧表示)


**ls**と**lsa**コマンドは、一連の現在のソース ファイルからの線の表示し、現在のソース行番号に進んでください。

```dbgcmd
ls [.] [first] [, count] 
lsa [.] address [, first [, count]] 
```

## <a name="span-idddkcmdlistsourcelinesdbgspanspan-idddkcmdlistsourcelinesdbgspanparameters"></a><span id="ddk_cmd_list_source_lines_dbg"></span><span id="DDK_CMD_LIST_SOURCE_LINES_DBG"></span>パラメーター


 **.**    
により、コマンドは、ソース ファイルを検索するデバッガー エンジンまたは[ **.srcpath (ソース パスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)コマンドを使用しています。 場合、期間 ( **.** ) は含まれず、 **ls**が最後に読み込まれたファイルを使用して、 [ **lsf (ソース ファイルの読み込み)** ](lsf--lsf---load-or-unload-source-file-.md)コマンド。

<span id="_______address______"></span><span id="_______ADDRESS______"></span> *address*   
ソースの表示の開始アドレスを指定します。

構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______first______"></span><span id="_______FIRST______"></span> *first*   
表示する最初の行を指定します。 既定値は、現在の行です。

<span id="_______count______"></span><span id="_______COUNT______"></span> *count*   
表示する行の数を指定します。 既定値は 20 (0x14) を使用して、既定値を変更していない限り、 [ **lsp-a** ](lsp--set-number-of-source-lines-.md)コマンド。

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

 

<a name="remarks"></a>コメント
-------

実行した後、 **ls**または**lsa**コマンド、現在の行がさらに 1 つ表示される最後の行として再定義します。 現在の行が後で使用される**ls**、 **lsa**、および[ **lsc** ](lsc--list-current-source-.md)コマンド。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**lsc (現在のソースの一覧)** ](lsc--list-current-source-.md)

[**lsf、lsf - (ロードまたはアンロード ソース ファイル)** ](lsf--lsf---load-or-unload-source-file-.md)

 

 







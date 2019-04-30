---
title: .srcfix、.lsrcfix (ソース サーバーの使用)
description: .Srcfix と .lsrcfix コマンドでは、ソース パスを移行元サーバーが使用されることを示すために自動的に設定します。
ms.assetid: e4cc3031-7990-4339-9dc2-f2c5a219a771
keywords:
- .srcfix、.lsrcfix (ソース サーバーを使用) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcfix, .lsrcfix (Use Source Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b5710055ed6656452b2cb2278c11f8e7baaa12f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338815"
---
# <a name="srcfix-lsrcfix-use-source-server"></a>.srcfix、.lsrcfix (ソース サーバーの使用)


**.Srcfix**と **.lsrcfix**コマンドは、移行元サーバーを使用することを示すソース パスを自動的に設定します。

```dbgcmd
.srcfix[+] [Paths] 
.lsrcfix[+] [Paths] 
```

## <a name="span-idddkmetausesourceserverdbgspanspan-idddkmetausesourceserverdbgspanparameters"></a><span id="ddk_meta_use_source_server_dbg"></span><span id="DDK_META_USE_SOURCE_SERVER_DBG"></span>パラメーター


<span id="______________"></span> **+**   
保持するには、既存のソース パスを原因と **; srv\\*** 末尾に追加します。 場合、 **+** が使用されていない既存のソース パスが置き換えられます。

<span id="_______Paths______"></span><span id="_______paths______"></span><span id="_______PATHS______"></span> *パス*   
新しいソース パスの末尾に追加する 1 つまたは複数の追加のパスを指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

**.Srcfix**コマンドはすべてのデバッガーで使用できます。 **.Lsrcfix**コマンドは、WinDbg でのみ使用でき、スクリプト ファイルでは使用できません。

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

リモート クライアントのローカル ソース パスの設定の詳細については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。 詳細については[SrcSrv](srcsrv.md)を参照してください[移行元サーバーを使用して](using-a-source-server.md)します。 詳細については、元のパスとローカルのソース パスは、次を参照してください。[ソース パス](source-path.md)します。 デバッガーからのリモート デバッグの実行中に使用できるコマンドの詳細については、次を参照してください。[リモート デバッグ セッションを制御する](controlling-a-remote-debugging-session.md)します。

<a name="remarks"></a>注釈
-------

追加すると`srv*`、デバッガーを使用して、ソース パスを[SrcSrv](srcsrv.md)対象モジュールのシンボル ファイルで指定された場所からソース ファイルを取得します。 使用して`srv*`ソース パスを使用して根本的に異なる`srv*`シンボル パスにします。 シンボル パスにと共にシンボル サーバーの場所を指定することができます、 `srv*` (たとえば、 `.sympath SRV* https://msdl.microsoft.com/download/symbols`)。 ソース パスが、srv\*だけで、その他のすべての要素からセミコロンで区切ってを意味します。

このコマンドは、デバッグのクライアントから発行されたときに **.srcfix**デバッグ サーバーで移行元サーバーを使用するソース パスを設定中に **.lsrcfix**はローカル コンピューターと同じです。

これらのコマンドと同じ、 [ **.srcpath (ソース パスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)と **.lsrcpath (ローカル ソース パスを設定する)** コマンドの後に、 **srv\\** * ソース パスの要素。 したがって、次の 2 つのコマンドは同等です。

```dbgcmd
.srcfix[+] [Paths] 
.srcpath[+] srv*[;Paths] 
```

同様に、次の 2 つのコマンドは同等です。

```dbgcmd
.lsrcfix[+] [Paths] 
.lsrcpath[+] srv*[;Paths] 
```

 

 






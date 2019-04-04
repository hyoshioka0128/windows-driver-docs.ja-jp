---
title: .servers (デバッグ サーバーの一覧)
description: .Servers コマンドには、このデバッガーで確立されているすべてのデバッグ サーバーが一覧表示します。
ms.assetid: bf65c6f7-9c59-4756-a667-8b896bd7ea2a
keywords:
- デバッグ サーバー (.servers) コマンドを一覧表示します。
- リモート デバッグ、デバッガーはデバッグ List Servers (.servers) コマンド
- .servers (デバッグ サーバーの一覧) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .servers (List Debugging Servers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab582243523d36d9e842f1d910026b6ae3672533
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528037"
---
# <a name="servers-list-debugging-servers"></a>.servers (デバッグ サーバーの一覧)


**.Servers**コマンドには、このデバッガーで確立されているすべてのデバッグ サーバーが一覧表示します。

```dbgcmd
.servers 
```

## <span id="ddk_meta_list_debugging_servers_dbg"></span><span id="DDK_META_LIST_DEBUGGING_SERVERS_DBG"></span>


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

サーバーのデバッグに関する詳細は、[リモート デバッグで、デバッガー](remote-debugging-through-the-debugger.md)を参照してください。

<a name="remarks"></a>注釈
-------

出力、 **.servers**コマンドには、このコマンドが実行されたデバッガーによって開始されたすべてのデバッグ サーバーが一覧表示します。 引数としてリテラル使用できるように、出力が書式設定は、リモートのコマンド ライン オプションの WinDbg ダイアログ ボックスに貼り付けるか。

各デバッグ サーバーが一意の ID で識別されます。 この ID を引数として使用できる、 [ **.endsrv (エンド デバッグ サーバー)** ](-endsrv--end-debugging-server-.md)デバッグ サーバーを終了する場合、コマンドします。

**.Servers**コマンドが、デバッガーの異なるインスタンスによって、このコンピューターで開始するデバッグ サーバーを一覧表示やはそのリストのプロセス サーバーまたは KD 接続サーバー。

 

 






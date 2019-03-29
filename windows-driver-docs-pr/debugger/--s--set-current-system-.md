---
title: s (現在のシステム設定)
description: S コマンドを設定または現在のシステム番号が表示されます。
ms.assetid: 33ad3a63-166f-4669-868c-49100c9b4d8c
keywords:
- s (現在のシステムのセット) の Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- s (Set Current System)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6079bff9140a042410252a0ecbee5da5eca6569f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570717"
---
# <a name="s-set-current-system"></a>||s (システム時刻の設定)

**| |s**コマンドを設定または現在のシステム番号が表示されます。

```dbgcmd
     ||System s 
     || s 
```

このコマンドを混同しないでください、 [ **s (メモリの検索)**](s--search-memory-.md)、 [ **~ s (変更の現在のプロセッサ)**](-s--change-current-processor-.md)、 [ **~ (設定現在のスレッド) s**](-s--set-current-thread-.md)、または[ **| s (現在のプロセスの設定)** ](-s--set-current-process-.md)コマンド。


## <a name="span-idddkcmdsetcurrentsystemdbgspanspan-idddkcmdsetcurrentsystemdbgspanparameters"></a><span id="ddk_cmd_set_current_system_dbg"></span><span id="DDK_CMD_SET_CURRENT_SYSTEM_DBG"></span>パラメーター


<span id="_______System______"></span><span id="_______system______"></span><span id="_______SYSTEM______"></span> *システム*   
アクティブ化するシステムの番号を指定します。 構文の詳細については、次を参照してください。[システム構文](system-syntax.md)します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>複数のターゲットのデバッグ</p></td>
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

**| |s**コマンドは、複数のターゲットをデバッグまたは複数のダンプ ファイルを操作するときに便利です。  この種のセッションの詳細については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

使用する場合、 **| |s**構文、デバッガーには、現在のシステムに関する情報が表示されます。

このコマンドでは、現在のシステム、プロセス、およびスレッドの現在の命令も逆アセンブルします。

 
**注**  コマンドのデバッグの種類ごとに異なる方法で動作しているために、ライブのターゲットと、ダンプ ターゲットをデバッグするときに、問題があります。 たとえば、使用する場合、 **g (移動)** コマンドの場合は、現在のシステムは、ダンプ ファイル、デバッガーが実行を開始がすることはできません戻るデバッガーに割り込む、break コマンドが認識されないため、ダンプ ファイルのデバッグの有効とします。










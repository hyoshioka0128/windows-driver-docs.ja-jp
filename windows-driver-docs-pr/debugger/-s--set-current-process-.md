---
title: s (現在のプロセスを設定する)
description: S コマンドを設定または現在のプロセス数が表示されます。
ms.assetid: 6b4d8e00-426c-496b-9c52-c60faeb0c975
keywords:
- s (現在のプロセスのセット) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- s (Set Current Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2fb36aa01a80ba7e779fcf808aa726d5dda4609
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579692"
---
# <a name="s-set-current-process"></a>|s (現在のプロセスの設定)


**| S**コマンドを設定または現在のプロセス数が表示されます。

このコマンドを混同しないでください、 [ **s (メモリの検索)**](s--search-memory-.md)、 [ **~ s (変更の現在のプロセッサ)**](-s--change-current-processor-.md)、 [ **~ s (現在のスレッドのセット)**](-s--set-current-thread-.md)、または[ **| |s (現在のシステムの設定)** ](--s--set-current-system-.md)コマンド。

```dbgcmd
|Process s 
| s 
```

## <a name="span-idddkcmdsetcurrentprocessdbgspanspan-idddkcmdsetcurrentprocessdbgspanparameters"></a><span id="ddk_cmd_set_current_process_dbg"></span><span id="DDK_CMD_SET_CURRENT_PROCESS_DBG"></span>パラメーター


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
設定または表示するプロセスを指定します。 構文の詳細については、次を参照してください。[プロセス構文](process-syntax.md)します。

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
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

表示するプロセスとスレッドを制御するための他の方法の詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>コメント
-------

プロセスは、ユーザー モードでのみ指定できます。

使用する場合、 **| s**構文、デバッガーは、現在のプロセスに関する情報を表示します。

このコマンドでは、現在のシステム、プロセス、およびスレッドの現在の命令も逆アセンブルします。

 

 






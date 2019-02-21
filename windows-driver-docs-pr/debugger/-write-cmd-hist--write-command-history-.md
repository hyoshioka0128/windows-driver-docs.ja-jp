---
title: .write_cmd_hist (書き込みコマンド履歴)
description: .Write_cmd_hist コマンドは、デバッガー コマンド ウィンドウの履歴全体をファイルに書き込みます。
ms.assetid: 7d512f0c-56cd-48e5-b618-d5615113f065
keywords:
- .write_cmd_hist (書き込みコマンド履歴) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .write_cmd_hist (Write Command History)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00dd73e25f967e25d6ded22580ae45e5cb6640ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528393"
---
# <a name="writecmdhist-write-command-history"></a>.write\_cmd\_hist (書き込みコマンド履歴)


**.Write\_cmd\_hist**コマンドでは、デバッガー コマンド ウィンドウの履歴全体をファイルに書き込みます。

```dbgcmd
.write_cmd_hist Filename 
```

## <a name="span-idddkmetacmdhistwritecommandhistorydbgspanspan-idddkmetacmdhistwritecommandhistorydbgspanparameters"></a><span id="ddk_meta_cmd_hist_write_command_history_dbg"></span><span id="DDK_META_CMD_HIST_WRITE_COMMAND_HISTORY_DBG"></span>パラメーター


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *ファイル名*   
作成されるファイルのファイル名とパスを指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、WinDbg でのみ使用でき、スクリプト ファイルでは使用できません。

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

 

 

 






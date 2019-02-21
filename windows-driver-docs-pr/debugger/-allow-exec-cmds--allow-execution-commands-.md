---
title: .allow_exec_cmds (コマンドの実行を許可する)
description: .Allow_exec_cmds コマンドでは、実行コマンドを使用できるかどうかを制御します。
ms.assetid: c6e37cf1-42cc-4f82-9eb8-d252f0b6e196
keywords:
- .allow_exec_cmds (コマンドの実行を許可する) Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .allow_exec_cmds (Allow Execution Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b81c201ee4429b131c1e7f41f00814cae541f724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552409"
---
# <a name="allowexeccmds-allow-execution-commands"></a>.allow\_exec\_コマンド (実行コマンドを許可する)


**.Allow\_exec\_コマンド**コマンドの実行コマンドを使用するかどうかを制御します。

```dbgcmd
.allow_exec_cmds 0 
.allow_exec_cmds 1 
.allow_exec_cmds 
```

## <a name="span-idddkmetaallowexecutioncommandsdbgspanspan-idddkmetaallowexecutioncommandsdbgspanparameters"></a><span id="ddk_meta_allow_execution_commands_dbg"></span><span id="DDK_META_ALLOW_EXECUTION_COMMANDS_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
実行コマンドが使用されないようにします。

<span id="_______1______"></span> **1**   
により使用されるコマンドを実行できます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードとカーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

実行コマンドの完全な一覧を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>注釈
-------

パラメーターなしで **.allow\_exec\_コマンド**実行コマンドが現在許可されているかどうかが表示されます。

実行コマンドが含まれます[ **g (移動)**](g--go-.md)、 [ **t (トレース)**](t--trace-.md)、 [ **p (ステップ)** ](p--step-.md)、および、その他のコマンドまたは WinDbg のグラフィカル インターフェイスのアクションを実行するターゲットを原因となります。

 

 






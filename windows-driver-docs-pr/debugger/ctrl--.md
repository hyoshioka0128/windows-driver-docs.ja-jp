---
title: CTRL + \ (現在のデバッガーのデバッグ)
description: CTRL + \ キーの組み合わせ CDB; の新しいインスタンスを起動します。現在のデバッガーは、この新しいデバッガーは、そのターゲットとして受け取ります。
ms.assetid: c0c63af5-712c-47b6-8811-81e441ddb3df
keywords:
- CTRL + (現在のデバッガーをデバッグする) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+\ (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f377f5f248a0ea1d0a623f71b011d3dba8d7dc4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558111"
---
# <a name="ctrl-debug-current-debugger"></a>CTRL +\\ (現在のデバッガーのデバッグ)


**CTRL +\\** キー CDB の新しいインスタンスを起動する。 この新しいのデバッガーはそのターゲットとしての現在のデバッガーを取得します。

```dbgcmd
CTRL+\  ENTER 
```

## <span id="ddk_meta_ctrl_p_dbg"></span><span id="DDK_META_CTRL_P_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>デバッガー</strong></td>
<td align="left"><p>CDB、NTSD、KD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

新しい CDB を起動するのと同じ、 [ **remote.exe** ](the-remote-exe-utility.md)ユーティリティ、および既に実行されているデバッガーをデバッグするために使用します。

[**CTRL +\\**  ](ctrl-alt--.md)に似ていますが、 [ **.dbgdbg (現在のデバッガーのデバッグ)** ](-dbgdbg--debug-current-debugger-.md)コマンド。

 

 






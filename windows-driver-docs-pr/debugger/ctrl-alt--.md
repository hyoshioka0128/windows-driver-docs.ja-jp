---
title: CTRL + ALT + \ (現在のデバッガーのデバッグ)
description: CTRL + ALT + \ キーの組み合わせ CDB; の新しいインスタンスを起動します。現在のデバッガーは、この新しいデバッガーは、そのターゲットとして受け取ります。
ms.assetid: 0a36baa4-fe40-4498-9cf8-ae81497f1dda
keywords:
- CTRL + ALT + (現在のデバッガーをデバッグする) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+ALT+\ (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de0743fec4ff83632b8a67676265b0797dbb866b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374431"
---
# <a name="ctrlalt-debug-current-debugger"></a>CTRL + ALT +\\ (現在のデバッガーのデバッグ)


**CTRL + ALT +\\** キー CDB の新しいインスタンスを起動する。 この新しいのデバッガーはそのターゲットとしての現在のデバッガーを取得します。

```dbgcmd
CTRL+ALT+\ 
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
<td align="left"><p>WinDbg</p></td>
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

**CTRL + ALT +\\** に似ていますが、 [ **.dbgdbg (現在のデバッガーのデバッグ)** ](-dbgdbg--debug-current-debugger-.md)コマンド、ただし**CTRL + ALT +\\** が、デバッガーのコマンドラインが利用できない場合に使用されることができますを活用します。

 

 






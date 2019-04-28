---
title: Ctrl + B (ローカル デバッガーの終了)
description: Ctrl キーを押しながら B キーが原因と、デバッガーが突然終了します。 これには、リモート デバッグ セッションは終了しません。
ms.assetid: f70f4c40-244f-4abf-982f-d738800ac621
keywords:
- CTRL + B (Quit ローカル デバッガー) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+B (Quit Local Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9fa104f8e74e3cbf1e6caf6580588f09d9586ea0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374965"
---
# <a name="ctrlb-quit-local-debugger"></a>Ctrl + B (ローカル デバッガーの終了)


Ctrl キーを押しながら B キーが原因と、デバッガーが突然終了します。 これには、リモート デバッグ セッションは終了しません。

```dbgcmd
CTRL+B  ENTER 
```

## <span id="ddk_meta_ctrl_b_dbg"></span><span id="DDK_META_CTRL_B_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>デバッガー</strong></p></td>
<td align="left"><p>CDB と KD のみ</p></td>
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

CDB、 [ **q (終了)** ](q--qq--quit-.md)を終了するコマンドを使用する必要があります。 CTRL + B は、デバッガーが応答していない場合にのみ使用する必要があります。

KD で、 **q**コマンドは、デバッグ セッションを終了し、ロックされているターゲット コンピューターのままにします。 (そのために、新しいデバッガーが接続できる) は、デバッグ セッションを維持する必要がある場合、またはを実行しているターゲット コンピューターのままにする必要がある場合は、CTRL キーを押しながら B キーを使用する必要があります。

同等のコマンドには、WinDbg で[ファイル |終了](file---exit.md)または alt キーを押しながら f4 キー。

 

 






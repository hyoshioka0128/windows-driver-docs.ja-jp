---
title: .flash_on_break (中断時にフラッシュ)
description: .Flash_on_break コマンドでは、WinDbg を最小化し、ターゲットの区切りときに WinDbg タスク バーのエントリが点滅するかどうかを指定します。
ms.assetid: b2f0a8c5-5b32-44f4-9546-c75859476ce0
keywords:
- .flash_on_break (flash の中断) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .flash_on_break (Flash on Break)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b735bbfeb806737ec1a39a8518e8ca5f357dc51
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581352"
---
# <a name="flashonbreak-flash-on-break"></a>.flash\_で\_break (中断で Flash)


**.Flash\_で\_break**コマンドでは、WinDbg を最小化し、ターゲットの区切りときに WinDbg タスク バーのエントリが点滅するかどうかを指定します。

```dbgcmd
.flash_on_break on 
.flash_on_break off 
.flash_on_break 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______on______"></span><span id="_______ON______"></span> **on**   
フラッシュ WinDbg が最小化され、ターゲットは、デバッガーを中断する場合に、WinDbg タスク バーのエントリをによりします。 これは、WinDbg の既定の動作です。

<span id="_______off______"></span><span id="_______OFF______"></span> **オフ**   
点滅 WinDbg タスク バーのエントリを防ぎます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

**.Flash\_で\_break**コマンドは、WinDbg でのみ使用できます。 このコマンドは、スクリプト ファイルで使用できません。

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

使用する場合、 **.flash\_で\_break**パラメーターを指定せずコマンドと、デバッガーは、現在フラッシュ設定を表示します。

 

 






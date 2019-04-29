---
title: .time (システム時刻の表示)
description: .Time コマンドでは、システム時刻の変数に関する情報が表示されます。
ms.assetid: d8024f84-98ff-4017-81c5-8a08973f9e4b
keywords:
- システム時刻 (.time) コマンドが表示されます。
- .time (表示のシステム時刻) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .time (Display System Time)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c368099fceda7d57bc51d0509de68e391b30a40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334228"
---
# <a name="time-display-system-time"></a>.time (システム時刻の表示)


**.Time**コマンドがシステム時間環境変数に関する情報を表示します。

```dbgcmd
.time [-h Hours]
```

## <a name="span-idddkmetadisplaysystemtimedbgspanspan-idddkmetadisplaysystemtimedbgspanparameters"></a><span id="ddk_meta_display_system_time_dbg"></span><span id="DDK_META_DISPLAY_SYSTEM_TIME_DBG"></span>パラメーター


<span id="_______-h________Hours______"></span><span id="_______-h________hours______"></span><span id="_______-H________HOURS______"></span> **-h** **** *時間*   
時間、グリニッジ標準時からのオフセットを指定します。 負の値を*時間*かっこで囲む必要があります。

<span></span>  

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム時間環境変数は、パフォーマンス カウンターの動作を制御します。

カーネル モードの例を示します。

```dbgcmd
kd> .time
Debug session time: Wed Jan 31 14:47:08 2001
System Uptime: 0 days 2:53:56 
```

ユーザー モードで例を示します。

```dbgcmd
0:000> .time
Debug session time: Mon Apr 07 19:10:50 2003
System Uptime: 4 days 4:53:56.461
Process Uptime: 0 days 0:00:08.750
  Kernel time: 0 days 0:00:00.015
  User time: 0 days 0:00:00.015
```

 

 






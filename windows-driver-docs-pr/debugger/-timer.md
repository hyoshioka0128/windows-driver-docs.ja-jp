---
title: タイマー
description: タイマー拡張機能は、すべてのシステムの詳細な一覧を表示します。 タイマーを使用します。
ms.assetid: 795bdfe1-1ee4-4bf2-9fcd-80415fe84754
keywords:
- Windows デバッグ タイマー
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- timer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1174b5ca33f16f2137e6529c78b9d4b78096c856
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334208"
---
# <a name="timer"></a>!timer


**! タイマー**拡張機能は、すべてのシステムの詳細な一覧を表示します。 タイマーを使用します。

```dbgcmd
!timer 
```

## <span id="ddk__timer_dbg"></span><span id="DDK__TIMER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

タイマー オブジェクトについては、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

**! タイマー**拡張機能には、システムのすべてのタイマー オブジェクトを格納するタイマー ツリーが表示されます。

以下に例を示します。

```dbgcmd
kd> !timer
Dump system timers

Interrupt time: 9f760774 00000000 [12/ 8/2000 10:59:22.685 (Pacific Standard Time)]

List Timer    Interrupt Low/High     Fire Time              DPC/thread
 0 8016aea0 P 9fbd8e00 00000000 [12/ 8/2000 10:59:23.154]  ntoskrnl!PopScanIdleList 
  1 8257f118   e4e4225a 00000000 [12/ 8/2000 11:01:19.170]  thread 8257f030 
 3 80165fc0   286be1c9 0000594a [ 4/ 1/2001 01:59:59.215]  ntoskrnl!ExpTimeZoneDpcRoutine 
    80165f40   2a7bf8d9 006f105e [12/31/2099 23:59:59.216]  ntoskrnl!ExpCenturyDpcRoutine 
  5 825a0bf8   a952e1c2 00000000 [12/ 8/2000 10:59:39.232]  thread 825a0b10 
 10 8251c7a8   41f54d84 00000001 [12/ 8/2000 11:03:55.310]  thread 8251c6c0 
    8249fe88   41f54d84 00000001 [12/ 8/2000 11:03:55.310]  thread 8249fda0 
 11 8250e7e8   bc73ffde 00000000 [12/ 8/2000 11:00:11.326]  thread 8250e700 

.....

237 82757070   9f904152 00000000 [12/ 8/2000 10:59:22.857]  +f7a56f2e 
    82676348   9f904152 00000000 [12/ 8/2000 10:59:22.857]  +fe516352 
    82728b78   9f904152 00000000 [12/ 8/2000 10:59:22.857]  +fe516352 
238 fe4b5d78   9f92a3ac 00000000 [12/ 8/2000 10:59:22.873]  thread 827ceb10 
    801658f0   9f92a3ac 00000000 [12/ 8/2000 10:59:22.873]  ntoskrnl!CcScanDpc 
239 8259ad40   765a6f19 00000bba [12/23/2000 09:07:22.900]  thread 825d3670 
250 826d42f0   1486bed8 80000000 [         NEVER         ]  thread 825fa030 

Total Timers: 193, Maximum List: 7
Current Hand: 226, Maximum Search: 0

Wakeable timers:
```

 

 






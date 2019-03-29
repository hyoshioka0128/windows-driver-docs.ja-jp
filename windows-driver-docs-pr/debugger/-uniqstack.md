---
title: uniqstack
description: Uniqstack 拡張機能は、重複が表示されるスタックを除く、現在のプロセスで、すべてのスレッドのスタックのすべてを表示します。
ms.assetid: c7502106-90b7-4fec-aa6b-394967ed2cfb
keywords:
- Windows デバッグ uniqstack
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- uniqstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b31e61cb711fdde9c55c8181d1ba852228ab68a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574662"
---
# <a name="uniqstack"></a>!uniqstack


**! Uniqstack**拡張機能はすべてのスレッドのスタックのすべての重複が表示されるスタックを除く、現在のプロセスが表示されます。

```dbgcmd
!uniqstack [ -b | -v | -p ] [ -n ]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
各関数に渡される最初の 3 つのパラメーターを含める表示をによりします。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
フレーム ポインターの省略 (FPO) 情報が追加ディスプレイをによりします。 X86 ベースのプロセッサで呼び出し元の規則の情報も表示されます。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
スタック トレース内の各関数が呼び出される完全なパラメーターを指定するディスプレイをによりします。 この一覧には、各パラメーターのデータ型、名前、および値が含まれます。 *これには、完全なシンボル情報が必要です。*

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
エラーの原因のフレーム数を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

この拡張機能はのような[ **k、kb、kc、kd、kp、kP、kv (Stack Backtrace の表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド、重複するスタックが表示されない点が異なります。

例:

```dbgcmd
0:000> !uniqstack
Processing 14 threads, please wait

.  0  Id: f0f0f0f0.15c Suspend: 1 Teb: 00000000`7fff8000 Unfrozen
      Priority: 0
Child-SP          Child-BSP         RetAddr
00000000`0006e5e0 00000000`00070420 00000000`6b009840
00000000`0006e600 00000000`000703d0 00000000`6b03db00
00000000`0006e950 00000000`000703b0 00000000`6b008520
00000000`0006e950 00000000`00070368 00000000`6b1845e0
00000000`0006e9b0 00000000`00070310 00000000`6b009980
00000000`0006e9d0 00000000`000702d0 00000000`6b009ff0
00000000`0006e9e0 00000000`00070248 00000000`77ea4a10
00000000`0006f290 00000000`000700e0 00000000`77ea5d60
00000000`0006f4c0 00000000`00070028 00000000`77ed6000
00000000`0006f550 00000000`00070000 00000000`77ed9000
00000000`0006f550 00000000`00070000 00000000`77ca78a0
00000000`0006fff0 00000000`00070000 00000000`00000000

.  1  Id: f0f0f0f0.718 Suspend: 1 Teb: 00000000`7fff4000 Unfrozen
      Priority: 0
Child-SP          Child-BSP         RetAddr
00000000`0043eb50 00000000`00440250 00000000`6b008520
00000000`0043eb80 00000000`00440208 00000000`6b1845e0
00000000`0043ebe0 00000000`004401a8 00000000`6b009980
00000000`0043ec00 00000000`00440168 00000000`6b009ff0
00000000`0043ec10 00000000`004400e0 00000000`77ea5f50
00000000`0043f4c0 00000000`00440028 00000000`77ed6000
00000000`0043f550 00000000`00440000 00000000`77ed9000
00000000`0043f550 00000000`00440000 00000000`7de05690
00000000`0043fff0 00000000`00440000 00000000`00000000

. 13  Id: f0f0f0f0.494 Suspend: 1 Teb: 00000000`7ef98000 Unfrozen
      Priority: 0
Child-SP          Child-BSP         RetAddr
00000000`00feffe0 00000000`00ff0040 00000000`77e94f30
00000000`00feffe0 00000000`00ff0040 00000000`00000000

Total threads: 14
Duplicate callstacks: 11 (windbg thread #s follow):
2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
```

 

 






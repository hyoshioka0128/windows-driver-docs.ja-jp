---
title: popolicy
description: Popolicy 拡張機能では、ターゲット コンピューターの電源ポリシーが表示されます。
ms.assetid: 4917e6e8-982f-41d7-acd8-047e590e1253
keywords:
- Windows デバッグ popolicy
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- popolicy
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f54b19ac1001c3adab38195f033986d92b297f52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335781"
---
# <a name="popolicy"></a>!popolicy


**! Popolicy**拡張機能には、ターゲット コンピューターの電源ポリシーが表示されます。

```dbgcmd
!popolicy [Address]
```

## <a name="span-idddkpopolicydbgspanspan-idddkpopolicydbgspanparameters"></a><span id="ddk__popolicy_dbg"></span><span id="DDK__POPOLICY_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する電源ポリシー構造体のアドレスを指定します。 これを省略した場合、nt!PopPolicy が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

表示するには、システムの電源機能を使用して、 [ **! pocaps** ](-pocaps.md)拡張機能コマンド。 電源機能、および電源ポリシーについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

このコマンドの出力の例を次に示します。

```dbgcmd
kd> !popolicy
SYSTEM_POWER_POLICY (R.1) @ 0x80164d58
  PowerButton:      Shutdown  Flags: 00000003   Event: 00000000   Query UI
  SleepButton:          None  Flags: 00000003   Event: 00000000   Query UI
  LidClose:             None  Flags: 00000001   Event: 00000000   Query
  Idle:                 None  Flags: 00000001   Event: 00000000   Query
  OverThrottled:        None  Flags: c0000004   Event: 00000000   Override NoWakes Critical
  IdleTimeout:             0  IdleSensitivity:        50%
  MinSleep:               S0  MaxSleep:               S0
  LidOpenWake:            S0  FastSleep:              S0
  WinLogonFlags:           1  S4Timeout:               0
  VideoTimeout:            0  VideoDim:               209
  SpinTimeout:             0  OptForPower:             1
  FanTolerance:            0% ForcedThrottle:          0%
  MinThrottle:             0%
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[プラグ アンド プレイと電源のデバッガー コマンド](plug-and-play-and-power-debugger-commands.md)

 

 







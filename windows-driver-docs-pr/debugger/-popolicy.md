---
title: popolicy
description: Popolicy 拡張機能には、対象のコンピューターの電源ポリシーが表示されます。
ms.assetid: 4917e6e8-982f-41d7-acd8-047e590e1253
keywords:
- popolicy Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- popolicy
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 03be5afb3b2b22e3de89b76a045157e2f5c091ff
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025184"
---
# <a name="popolicy"></a>!popolicy


**! Popolicy**拡張機能には、対象のコンピューターの電源ポリシーが表示されます。

```dbgcmd
!popolicy [Address]
```

## <a name="span-idddk__popolicy_dbgspanspan-idddk__popolicy_dbgspanparameters"></a><span id="ddk__popolicy_dbg"></span><span id="DDK__POPOLICY_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示する電源ポリシー構造のアドレスを指定します。 これを省略すると、nt!PopPolicy が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

システムの電源機能を表示するには、 [ **! pocaps**](-pocaps.md) extension コマンドを使用します。 電源機能と電源ポリシーの詳細については、Windows Driver Kit (WDK) のドキュメントと*Microsoft windows の内部構造*を参照してください。これには、Mark Russinovich と David ソロモンが使用されます。

<a name="remarks"></a>コメント
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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[プラグアンドプレイと Power Debugger のコマンド](plug-and-play-and-power-debugger-commands.md)

 

 







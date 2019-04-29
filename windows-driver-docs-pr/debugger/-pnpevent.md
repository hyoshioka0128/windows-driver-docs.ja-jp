---
title: pnpevent
description: Pnpevent 拡張機能では、プラグ アンド プレイ デバイスのイベント キューが表示されます。
ms.assetid: 5f70fbf8-1313-4238-a917-c3fba8c80927
keywords:
- Windows デバッグ pnpevent
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pnpevent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 19c66eea6a61217ce7d7ca7c8fd498b28c7caeae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334357"
---
# <a name="pnpevent"></a>!pnpevent


**! Pnpevent**拡張機能には、プラグ アンド プレイ デバイスのイベント キューが表示されます。

```dbgcmd
!pnpevent [DeviceEvent]
```

## <a name="span-idddkpnpeventdbgspanspan-idddkpnpeventdbgspanparameters"></a><span id="ddk__pnpevent_dbg"></span><span id="DDK__PNPEVENT_DBG"></span>パラメーター


<span id="_______DeviceEvent______"></span><span id="_______deviceevent______"></span><span id="_______DEVICEEVENT______"></span> *DeviceEvent*   
表示するデバイス イベントのアドレスを指定します。 これは、0 または省略すると、キュー内のすべてのデバイス イベントのツリーが表示されます。

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

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 プラグ アンド プレイ ドライバーについては、Windows Driver Kit (WDK) ドキュメントを参照してください。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[プラグ アンド プレイと電源のデバッガー コマンド](plug-and-play-and-power-debugger-commands.md)

 

 







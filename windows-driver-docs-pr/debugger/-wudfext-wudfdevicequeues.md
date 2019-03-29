---
title: wudfext.wudfdevicequeues
description: Wudfext.wudfdevicequeues 拡張機能では、デバイスのすべての I/O キューに関する情報が表示されます。
ms.assetid: 985e6d93-018f-436a-a75c-088251398539
keywords:
- デバッグ wudfext.wudfdevicequeues Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdevicequeues
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef0bce7454c02dd7e0fcc096a128aac9e9b173e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578956"
---
# <a name="wudfextwudfdevicequeues"></a>!wudfext.wudfdevicequeues


**! Wudfext.wudfdevicequeues**拡張機能は、デバイスのすべての I/O キューに関する情報を表示します。

```dbgcmd
!wudfext.wudfdevicequeues pWDFDevice
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pWDFDevice______"></span><span id="_______pwdfdevice______"></span><span id="_______PWDFDEVICE______"></span> *pWDFDevice*   
アドレスを指定します、 **IWDFDevice**関連付けられている I/O キューのすべてに関する情報を表示するためのインターフェイス。 [ **! Wudfext.wudfdriverinfo** ](-wudfext-wudfdriverinfo.md)拡張機能コマンドのアドレスを決定する**IWDFDevice**します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>コメント
-------

例を次に、 **! wudfext.wudfdevicequeues**表示。

```dbgcmd
## kd> !wudfdevicequeues 0xf2f80 
--------------------------------------------------
Queue: 1 (!wudfqueue 0x000f3500)
    WdfIoQueueDispatchSequential, POWER MANAGED, WdfIoQueuePowerOn, CAN ACCEPT, CAN DISPATCH
    Number of driver owned requests: 1
      IWDFIoRequest 0x000fa7c0     CWdfIoRequest 0x000fa748
    Number of waiting requests: 199
      IWDFIoRequest 0x000fa908     CWdfIoRequest 0x000fa890
      IWDFIoRequest 0x000faa50     CWdfIoRequest 0x000fa9d8
...
      IWDFIoRequest 0x000fa678     CWdfIoRequest 0x000fa600
    Driver's callback interfaces.
      IQueueCallbackRead 0x000f343c
      IQueueCallbackDeviceIoControl 0x000f3438
      IQueueCallbackWrite 0x000f3440
```

 

 






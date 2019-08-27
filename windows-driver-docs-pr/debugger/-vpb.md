---
title: vpb
description: Vpb 拡張機能により、ボリュームパラメーターブロック (VPB) が表示されます。
ms.assetid: 978d4ec8-6141-4656-9e5c-266de91c9440
keywords:
- vpb Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vpb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90f04f4146409059716449aab33c9070a7b3e1df
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025152"
---
# <a name="vpb"></a>!vpb


**! Vpb**拡張機能により、ボリュームパラメーターブロック (vpb) が表示されます。

```dbgcmd
!vpb Address
```

## <a name="span-idddk__vpb_dbgspanspan-idddk__vpb_dbgspanparameters"></a><span id="ddk__vpb_dbg"></span><span id="DDK__VPB_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
VPB の16進数のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

VPBs の詳細については、「Windows Driver Kit (WDK)」のドキュメントと*Microsoft windows の内部*(Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

次に例を示します。 まず、デバイスツリーが[ **! devnode**](-devnode.md)拡張機能と共に表示されます。

```dbgcmd
kd> !devnode 0 1
Dumping IopRootDeviceNode (= 0x80e203b8)
DevNode 0x80e203b8 for PDO 0x80e204f8
  InstancePath is "HTREE\ROOT\0"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  DevNode 0x80e56dc8 for PDO 0x80e56f18
    InstancePath is "Root\dmio\0000"
    ServiceName is "dmio"
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)
  DevNode 0x80e56ae8 for PDO 0x80e56c38
    InstancePath is "Root\ftdisk\0000"
    ServiceName is "ftdisk"
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)
 DevNode 0x80e152a0 for PDO 0x80e15cb8
      InstancePath is "STORAGE\Volume\1&30a96598&0&Signature5C34D70COffset7E00Length60170A00"
      ServiceName is "VolSnap"
      TargetDeviceNotify List - f 0xe1250938  b 0xe14b9198
      State = DeviceNodeStarted (0x308)
      Previous State = DeviceNodeEnumerateCompletion (0x30d)
    .....
```

一覧に表示されている最後のデバイスノードはボリュームです。 [ **! Devobj**](-devobj.md)拡張機能を使用して、その物理デバイスオブジェクト (PDO) を確認します。

```dbgcmd
kd> !devobj 80e15cb8
Device object (80e15cb8) is for:
 HarddiskVolume1 \Driver\Ftdisk DriverObject 80e4e248
Current Irp 00000000 RefCount 14 Type 00000007 Flags 00001050
Vpb 80e15c30 DevExt 80e15d70 DevObjExt 80e15e40 Dope 80e15bd8 DevNode 80e152a0 
ExtensionFlags (0000000000)  
AttachedDevice (Upper) 80e14c60 \Driver\VolSnap
Device queue is not busy.
```

このリストには、このデバイスの VPB のアドレスが含まれています。 このアドレスは、 **! vpb**拡張機能と共に使用します。

```dbgcmd
kd> !vpb 80e15c30
Vpb at 0x80e15c30
Flags: 0x1 mounted 
DeviceObject: 0x80de5020
RealDevice:   0x80e15cb8
RefCount: 14
Volume Label:           MY-DISK-C
```

 

 






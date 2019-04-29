---
title: devobj
description: Devobj 拡張機能では、DEVICE_OBJECT 構造に関する詳細情報が表示されます。
ms.assetid: cf722d95-fbd3-4d80-8679-f8fb348ab4b0
keywords:
- Windows デバッグ devobj
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58357319ee5561ae646e9cb55c95b7064a0ba4b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336808"
---
# <a name="devobj"></a>!devobj


**! Devobj**拡張機能は、デバイスに関する詳細情報を表示します。\_オブジェクトの構造体。

```dbgcmd
!devobj DeviceObject 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
デバイス オブジェクトを指定します。 この構造体の 16 進数のアドレスまたはデバイスの名前を指定できます。

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

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)例と、この拡張機能コマンドのアプリケーション。 デバイス オブジェクトについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

場合*デバイス オブジェクト*デバイスの名前を指定しますが、プレフィックス、プレフィックスを提供しない"\\デバイス\\"と見なされます。 このコマンドでかどうかをチェックする注*デバイス オブジェクト*式エバリュエーターを使用する前に有効なアドレスまたはデバイス名は、します。

表示される情報には、デバイスのキュー内のデバイスの現在の IRP については、オブジェクトのデバイス名と、保留中の Irp のアドレスの一覧が含まれます。 ("AttachedDevice"として表示)、このオブジェクトの上に階層化デバイス オブジェクトと ("AttachedTo"として表示)、このオブジェクトの下の階層に関する情報も含まれています。

デバイス オブジェクトのアドレスを使用して取得することができます、 [ **! drvobj** ](-drvobj.md)または[ **! devnode** ](-devnode.md)拡張機能。

1 つの例を次に示します。

```dbgcmd
kd> !devnode
Dumping IopRootDeviceNode (= 0x80e203b8)
DevNode 0x80e203b8 for PDO 0x80e204f8
 Parent 0000000000   Sibling 0000000000   Child 0x80e56dc8
  InstancePath is "HTREE\ROOT\0"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[04] = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[03] = DeviceNodeStarted (0x308)
  StateHistory[02] = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[01] = DeviceNodeStarted (0x308)
  StateHistory[00] = DeviceNodeUninitialized (0x301)
  StateHistory[19] = Unknown State (0x0)
  .....
  StateHistory[05] = Unknown State (0x0)
  Flags (0x00000131)  DNF_MADEUP, DNF_ENUMERATED, 
                      DNF_IDS_QUERIED, DNF_NO_RESOURCE_REQUIRED
  DisableableDepends = 11 (from children)

kd> !devobj 80e204f8
Device object (80e204f8) is for:
  \Driver\PnpManager DriverObject 80e20610
Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001000
DevExt 80e205b0 DevObjExt 80e205b8 DevNode 80e203b8 
ExtensionFlags (0000000000)  
Device queue is not busy.
```

 

 






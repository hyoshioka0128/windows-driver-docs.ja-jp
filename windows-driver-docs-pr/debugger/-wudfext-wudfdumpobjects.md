---
title: wudfext.wudfdumpobjects
description: Wudfext.wudfdumpobjects 拡張機能では、UMDF の未処理のオブジェクトが表示されます。
ms.assetid: 2ede7f2e-124c-494d-9188-5a28617a0bdb
keywords:
- デバッグ wudfext.wudfdumpobjects Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdumpobjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3aab71a2c315c9e5bd798a8fe0c7978cb11f9615
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538685"
---
# <a name="wudfextwudfdumpobjects"></a>!wudfext.wudfdumpobjects


**! Wudfext.wudfdumpobjects**拡張機能は、未処理の UMDF オブジェクトを表示します。

```dbgcmd
!wudfext.wudfdumpobjects ObjTrackerAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ObjTrackerAddress______"></span><span id="_______objtrackeraddress______"></span><span id="_______OBJTRACKERADDRESS______"></span> *ObjTrackerAddress*   
リークしているオブジェクトを追跡するためにアドレスを指定します。 このアドレスは、メモリ リークが発生した場合、デバッガーでドライバー停止メッセージに表示されます。

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
<td align="left"><p><strong>Windows XP UMDF バージョン 1.7 以降</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

場合は、UMDF オブジェクト追跡オプション (**TrackObjects**) が有効になって WDF Verifier で使用できます **! wudfext.wudfdumpobjects**にドライバーをアンロードした後に残っているオブジェクトがリークいずれかを参照してください。

場合、 **TrackObjects**オプションが有効になって、メモリ リークが検出されたときに、オブジェクトの追跡ツールのアドレスが自動的に表示されます。 このアドレスとして使用して*ObjTrackerAddress*の実行時に **! wudfext.wudfdumpobjects**します。

この拡張機能は、UMDF が「壊れていないデバッガーに場合でも、いつでも使用できます。

UMDF はバージョン 1.9 またはいずれかを使用する、 [ **! wudfext.umdevstack** ](-wudfext-umdevstack.md)または[ **! wudfext.umdevstacks** ](-wudfext-umdevstacks.md)アドレスを確認するにはオブジェクトの追跡ツール。 このアドレスに渡すことができます **! wudfext.wudfdumpobjects**します。 以下に例を示します。

```dbgcmd
0: kd> !umdevstacks 
Number of device stacks: 1
  Device Stack: 0x038c6f08    Pdo Name: \Device\USBPDO-11
    Number of UM devices: 1
    Device 0
      Driver Config Registry Path: WUDFOsrUsbFx2
      UMDriver Image Path: D:\Windows\system32\DRIVERS\UMDF\WUDFOsrUsbFx2.dll
      Fx Driver: IWDFDriver 0x3076ff0
      Fx Device: IWDFDevice 0x3082e70
        IDriverEntry: WUDFOsrUsbFx2!CMyDriver 0x0306eff8
      Open UM files (use !umfile <addr> for details): 
        0x04a8ef84
      Device XFerMode: CopyImmediately RW: Buffered CTL: Buffered
      Object Tracker Address: 0x03074fd8
        Object   Tracking ON
        Refcount Tracking OFF
    DevStack XFerMode: CopyImmediately RW: Buffered CTL: Buffered

0: kd> !wudfdumpobjects 0x03074fd8 
WdfTypeDriver    Object: 0x03076fb0, Interface: 0x03076ff0
WdfTypeDevice   Object: 0x03082e30, Interface: 0x03082e70
WdfTypeIoTarget Object: 0x03088f50, Interface: 0x03088f90
WdfTypeIoQueue                Object: 0x0308ce58, Interface: 0x0308ce98
WdfTypeIoQueue                Object: 0x03090e58, Interface: 0x03090e98
WdfTypeIoQueue                Object: 0x03092e58, Interface: 0x03092e98
WdfTypeIoTarget Object: 0x03098f40, Interface: 0x03098f80
WdfTypeFile         Object: 0x0309cfa0, Interface: 0x0309cfe0
WdfTypeUsbInterface         Object: 0x030a0f98, Interface: 0x030a0fd8
WdfTypeRequest Object: 0x030a2ef8, Interface: 0x030a2f38
WdfTypeIoTarget Object: 0x030a6f30, Interface: 0x030a6f70
WdfTypeIoTarget Object: 0x030aaf30, Interface: 0x030aaf70
WdfTypeIoTarget Object: 0x030aef30, Interface: 0x030aef70
WdfTypeRequest Object: 0x030c6ef8, Interface: 0x030c6f38
WdfTypeRequest Object: 0x030ceef8, Interface: 0x030cef38
WdfTypeMemoryObject    Object: 0x030d6fb0, Interface: 0x030d6ff0
WdfTypeMemoryObject    Object: 0x030dcfb0, Interface: 0x030dcff0
WdfTypeFile         Object: 0x030e4fa8, Interface: 0x030e4fe8
WdfTypeFile         Object: 0x030e6fa8, Interface: 0x030e6fe8
WdfTypeFile         Object: 0x030e8fa8, Interface: 0x030e8fe8
WdfTypeRequest Object: 0x030eaef8, Interface: 0x030eaf38
WdfTypeMemoryObject    Object: 0x030ecfb0, Interface: 0x030ecff0
WdfTypeMemoryObject    Object: 0x030eefb0, Interface: 0x030eeff0
```

 

 






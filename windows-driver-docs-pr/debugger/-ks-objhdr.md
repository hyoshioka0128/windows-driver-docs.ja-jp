---
title: ks.objhdr
description: Ks.objhdr 拡張機能では、指定されたファイル オブジェクトに関連付けられたオブジェクトのヘッダーをストリーミングするカーネルが表示されます。
ms.assetid: 105b1c03-fc89-4c0f-91d0-42e88f07c71c
keywords:
- デバッグ ks.objhdr Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.objhdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d1e656dcffb1b3e6ad5f3d4844b6b76274ba051
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552566"
---
# <a name="ksobjhdr"></a>!ks.objhdr


**! Ks.objhdr**拡張機能は、カーネルの指定されたファイル オブジェクトに関連付けられたオブジェクトのヘッダーをストリームを表示します。

```dbgcmd
!ks.objhdr FileObject [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
このパラメーターは、WDM ファイル オブジェクトへのポインターを指定します。 場合*FileObject*が無効で、コマンドには、エラーが返されます。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 値がの場合と同じ[ **! ks.dump**](-ks-dump.md)します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 値がの場合と同じ[ **! ks.dump**](-ks-dump.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

レベルし、フラグの **! ks.objhdr**で説明したものと同じ[ **! ks.dump**](-ks-dump.md)します。

出力[ **! ks.allstreams** ](-ks-allstreams.md)と[ **! ks.enumdevobj** ](-ks-enumdevobj.md) 、入力として使用できる **! ks.objhdr**. これを行う、 *avssamp*サンプルでは、たとえば、次のコマンドを発行します。

```dbgcmd
kd> !ks.allstreams
6 Kernel Streaming FDOs found:
    Functional Device 8299be18 [\Driver\smwdm]
    Functional Device 827c86d8 [\Driver\wdmaud]
    Functional Device 827c0f08 [\Driver\sysaudio]
    Functional Device 82424590 [\Driver\avssamp]
    Functional Device 82423720 [\Driver\MSPQM]
    Functional Device 82b91a88 [\Driver\MSPCLOCK]
kd> !ks.enumdevobj 82424590
WDM device object 82424590:
    Corresponding KSDEVICE        82427540
    Factory 8285baa4 [Descriptor f7a333c8] instances:
        82837a34 
kd> !ks.objhdr 82837a34 7
```

このコマンドの結果は、時間のかかる可能性があります。 出力を停止するには、CTRL + BREAK (WinDbg) または Ctrl + C (、CDB、NTSD KD) を発行します。

別の例を次に示します。

```dbgcmd
kd> !ks.objhdr 81D828B8 7
Adjusting file object 81D828B8 to object header 81BC1008

Object Header 81BC1008
    Associated Create Items:
        Create Item F9F77E98
            CreateFunction = ks!CKsFilter::DispatchCreatePin+0x00
            ObjectClass = {146F1A80-4791-11D0-A5D6-28DB04C10000}
            Flags = 0
    Child Create Handler List:
        Create Item F9F85AA0
            CreateFunction = ks!CKsPin::DispatchCreateAllocator+0x00
            ObjectClass = {642F5D00-4791-11D0-A5D6-28DB04C10000}
            Flags = 0
        Create Item F9F85AB8
            CreateFunction = ks!CKsPin::DispatchCreateClock+0x00
            ObjectClass = {53172480-4791-11D0-A5D6-28DB04C10000}
            Flags = 0
        Create Item F9F85AD0
            CreateFunction = ks!CKsPin::DispatchCreateNode+0x00
            ObjectClass = {0621061A-EE75-11D0-B915-00A0C9223196}
            Flags = 0
    DispatchTable:
        Dispatch Table F9F85AE8
            DeviceIoControl = ks!CKsPin::DispatchDeviceIoControl+0x00
            Read = ks!KsDispatchInvalidDeviceRequest+0x00
            Write = ks!KsDispatchInvalidDeviceRequest+0x00
            Flush = ks!KsDispatchInvalidDeviceRequest+0x00
            Close = ks!CKsPin::DispatchClose+0x00
            QuerySecurity = ks!KsDispatchQuerySecurity+0x00
            SetSecurity = ks!KsDispatchSetSecurity+0x00
            FastDeviceIoControl = ks!KsDispatchFastIoDeviceControlFailure+0x00
            FastRead = ks!KsDispatchFastReadFailure+0x00
            FastWrite = ks!KsDispatchFastReadFailure+0x00
    TargetState: KSTARGET_STATE_ENABLED
    TargetDevice: 00000000
    BaseDevice  : 81BBDF10
    Stack Depth : 1
    Corresponding AVStream object = 81A971B0
```

 

 






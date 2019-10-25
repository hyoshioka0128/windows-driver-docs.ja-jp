---
title: ioctldecode
description: Ioctldecode 拡張機能は、指定された IOCTL コードによって指定されたデバイスの種類、必要なアクセス、関数コード、および転送の種類を表示します。
ms.assetid: 50B12034-E5C7-43F2-A31E-AAC824A05D46
keywords:
- ioctldecode Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ioctldecode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e065c3f4576fe301895a1a950c601c9219db904
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826724"
---
# <a name="ioctldecode"></a>!ioctldecode


**! Ioctldecode**拡張機能では、指定された IOCTL コードによって指定された*デバイスの種類*、*必要なアクセス*、*関数コード*、および*転送の種類*が表示されます。 IOCTL 制御コードの詳細については、「 [I/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。

```dbgcmd
!ioctldecode IoctlCode 
```

## <a name="span-idddk__ioresdes_dbgspanspan-idddk__ioresdes_dbgspanparameters"></a><span id="ddk__ioresdes_dbg"></span><span id="DDK__IORESDES_DBG"></span>パラメータ


<span id="_______IoctlCode______"></span><span id="_______ioctlcode______"></span><span id="_______IOCTLCODE______"></span>*IoctlCode*   
16進の IOCTL コードを指定します。 [ **! Irp**](-irp.md)コマンドは、出力に IOCTL コードを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

IOCTL に関する情報を確認するには、まず、目的の IRP を見つけます。 [ **! Irpfind**](-irpfind.md)コマンドを使用して、目的の irp を見つけることができます。

Irp に関する情報を表示するには、 [ **! irp**](-irp.md)コマンドを使用します。

```dbgcmd
0: kd> !irp ffffd581a6c6cd30
Irp is active with 6 stacks 6 is current (= 0xffffd581a6c6cf68)
No Mdl: No System Buffer: Thread 00000000:  Irp stack trace.  
     cmd  flg cl Device   File     Completion-Context
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
[N/A(0), N/A(0)]
            0  0 00000000 00000000 00000000-00000000    

                                                Args: 00000000 00000000 00000000 00000000
>[IRP_MJ_INTERNAL_DEVICE_CONTROL(f), N/A(0)]
            0 e1 ffffd581a5fbd050 00000000 fffff806d2412cf0-ffffd581a5cce050 Success Error Cancel pending
                       \Driver\usbehci        (IopUnloadSafeCompletion)
                                                Args: ffffd581a6c61a50 00000000 0x220003 00000000
```

3番目の引数 (この場合は*0x220003*) が IOCTL コードです。 Ioctl コードを使用して、IOCTL に関する情報を表示します。この例では、ioctl [ **\_内部\_USB\_\_URB を送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)します。

```dbgcmd
0: kd> !ioctldecode 0x220003

IOCTL_INTERNAL_USB_SUBMIT_URB

Device Type    : 0x22 (FILE_DEVICE_WINLOAD) (FILE_DEVICE_USER_MODE_BUS) (FILE_DEVICE_USB) (FILE_DEVICE_UNKNOWN)
Method         : 0x3 METHOD_NEITHER 
Access         : FILE_ANY_ACCESS
Function       : 0x0
```

使用できない IOCTL コードを指定すると、この種類の出力が表示されます。

```dbgcmd
0: kd> !ioctldecode 0x1280ce

Unknown IOCTL  : 0x1280ce 

Device Type    : 0x12 (FILE_DEVICE_NETWORK)
Method         : 0x2 METHOD_OUT_DIRECT 
Access         : FILE_WRITE_ACCESS 
Function       : 0x33
```

IOCTL は識別されませんが、IOCTL フィールドに関する情報が表示されます。

**! Ioctldecode**コマンドで指定できるのは、パブリックに定義された ioctl のサブセットのみであることに注意してください。

Ioctl の詳細については、「 [I/o 制御コードの概要」を](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-i-o-control-codes)参照してください。

Irp と Ioctl に関する一般的な情報については、「Russinovich、David A ソロモン、および Alex Ionescu」を参照*してください*。

 

 






---
title: ioctldecode
description: Ioctldecode 拡張機能には、特定の IOCTL コードで指定されたデバイスの種類、アクセスのために必要な関数コードおよび転送の種類が表示されます。
ms.assetid: 50B12034-E5C7-43F2-A31E-AAC824A05D46
keywords:
- Windows デバッグ ioctldecode
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ioctldecode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6a26bead65df45b350293a05273b3fbb4e33b28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363166"
---
# <a name="ioctldecode"></a>!ioctldecode


**! Ioctldecode**拡張機能が表示されます、*デバイスの種類*、*アクセスのために必要な*、*関数コード*と*転送型*IOCTL の特定のコードで指定します。 詳細については、IOCTL 制御コードは、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)します。

```dbgcmd
!ioctldecode IoctlCode 
```

## <a name="span-idddkioresdesdbgspanspan-idddkioresdesdbgspanparameters"></a><span id="ddk__ioresdes_dbg"></span><span id="DDK__IORESDES_DBG"></span>パラメーター


<span id="_______IoctlCode______"></span><span id="_______ioctlcode______"></span><span id="_______IOCTLCODE______"></span> *IoctlCode*   
16 進数の IOCTL コードを指定します。 [ **! Irp** ](-irp.md)コマンドの出力で IOCTL コードを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

IOCTL で情報を表示するには、目的の IRP 最初見つけます。 使用することができます、 [ **! irpfind** ](-irpfind.md)関心のある irp を検索するコマンド。

使用して、 [ **! irp** ](-irp.md) irp に関する情報を表示するコマンド。

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

ここで表示されます。 3 番目の引数*0x220003*、IOCTL コードに示します。 ここでは、IOCTL に関する情報を表示する IOCTL コードを使用して[ **IOCTL\_内部\_USB\_送信\_URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)します。

```dbgcmd
0: kd> !ioctldecode 0x220003

IOCTL_INTERNAL_USB_SUBMIT_URB

Device Type    : 0x22 (FILE_DEVICE_WINLOAD) (FILE_DEVICE_USER_MODE_BUS) (FILE_DEVICE_USB) (FILE_DEVICE_UNKNOWN)
Method         : 0x3 METHOD_NEITHER 
Access         : FILE_ANY_ACCESS
Function       : 0x0
```

つまり使用できない IOCTL コードを指定する場合は、このタイプの出力が表示されます。

```dbgcmd
0: kd> !ioctldecode 0x1280ce

Unknown IOCTL  : 0x1280ce 

Device Type    : 0x12 (FILE_DEVICE_NETWORK)
Method         : 0x2 METHOD_OUT_DIRECT 
Access         : FILE_WRITE_ACCESS 
Function       : 0x33
```

IOCTL が識別されないが、IOCTL フィールドに関する情報が表示されます。

パブリックに定義された Ioctl のサブセットのみがで識別できることに注意してください、 **! ioctldecode**コマンド。

Ioctl の詳細については、次を参照してください。 [I/O 制御コードの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-i-o-control-codes)します。

Irp と Ioctl の概要についてを参照してください*Windows Internals* E. のある Mark Russinovich、David A. Solomon Alex Ionescu しています。

 

 






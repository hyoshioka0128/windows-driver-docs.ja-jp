---
title: 方法 2 を使用して IoIs32bitProcess
description: 方法 2 を使用して IoIs32bitProcess
ms.assetid: 41e9c0e6-59dd-4e01-9c82-5aba40d8b97f
keywords:
- 32 ビットの I/O は、WDK の 64 ビット、IoIs32bitProcess をサポートします。
- IoIs32bitProcess
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296c8ca40fc530fead46a45c5be8499c62e7d77a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382961"
---
# <a name="technique-2-using-iois32bitprocess"></a>方法 2: IoIs32bitProcess の使用





32 ビットおよび 64 ビットのアプリケーションからの I/O 要求を別の IOCTL または FSCTL コントロールのコードを定義するは実用的がない場合、ドライバーの I/O 要求を送信するアプリケーションの種類を決定することは左側です。 Microsoft Windows の 64 ビット バージョンには、新しいカーネル モードのルーチンが導入されています[ **IoIs32bitProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iois32bitprocess)、32 ビット ユーザー モード プロセスで現在の I/O 要求が発生したかどうかを検出します。 そのプロトタイプは。

```cpp
BOOLEAN
  IoIs32bitProcess(
    _In_opt_ PIRP Irp  // NULL for fast I/O call, IRP otherwise
    );
```

**IoIs32bitProcess**返します**TRUE**かどうか、現在の I/O 要求の発信元は、32 ビット ユーザー モード アプリケーション。

次のコード サンプルは、使用する方法を示します**IoIs32bitProcess**:

```cpp
typedef UINT32 POINTER_32 PVOID32;

typedef struct _IOCTL_PARAMETERS
{
    PVOID   Addr;
    SIZE_T  Length;
    HANDLE  Handle;
} IOCTL_PARAMETERS, *PIOCTL_PARAMETERS;

typedef struct _IOCTL_PARAMETERS_32
{
    PVOID32  Addr;
    INT32    Length;
    PVOID32  Handle;
} IOCTL_PARAMETERS_32, *PIOCTL_PARAMETERS_32;

...

IOCTL_PARAMETERS LocalParam;

if (IoIs32bitProcess(Irp))
{ 
    /* 32-bit process IOCTL */
    PIOCTL_PARAMETERS_32 params32;

    params32 = (PIOCTL_PARAMETERS_32)(Irp->AssociatedIrp.SystemBuffer);
    if (irpSp->Parameters.DeviceIoControl.InputBufferLength < sizeof(IOCTL_PARAMETERS_32))
    {
        status = STATUS_INVALID_PARAMETER;
    }
    else
    {
        LocalParam.Addr = Ptr32ToPtr(params32->Addr);
        LocalParam.Handle = Handle32ToHandle(params32->Handle);
        LocalParam.Length = params32->Length;

        /* Handle the IOCTL here. */
        ...

        status = STATUS_SUCCESS;
        Irp->IoStatus.Information = 0;
    }
}
else
{  
    /* 64-bit process IOCTL */
    PIOCTL_PARAMETERS params;

    params = (PIOCTL_PARAMETERS)(Irp->AssociatedIrp.SystemBuffer);
    if (irpSp->Parameters.DeviceIoControl.InputBufferLength < sizeof(IOCTL_PARAMETERS))
    {
        status = STATUS_INVALID_PARAMETER;
    }
    else
    {
        RtlCopyMemory(&LocalParam, params, sizeof(IOCTL_PARAMETERS));

        /* Handle the IOCTL here. */
        ...

        status = STATUS_SUCCESS;
    }
    Irp->IoStatus.Information = 0;
}
```

 

 





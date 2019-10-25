---
title: IoIs32bitProcess を使用した手法2
description: IoIs32bitProcess を使用した手法2
ms.assetid: 41e9c0e6-59dd-4e01-9c82-5aba40d8b97f
keywords:
- 32ビット i/o サポート WDK 64 ビット、IoIs32bitProcess
- IoIs32bitProcess
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cf5a4facc4fdce8c17abcf749f130b41796003c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838389"
---
# <a name="technique-2-using-iois32bitprocess"></a>方法 2: IoIs32bitProcess の使用





32ビットアプリケーションと64ビットアプリケーションからの i/o 要求に対して個別の IOCTL または FSCTL 制御コードを定義するのは現実的ではない場合、ドライバーは、i/o 要求を送信したアプリケーションの種類を特定するために残されています。 64ビットバージョンの Microsoft Windows では、現在の i/o 要求が32ビットのユーザーモードプロセスで発生したかどうかを検出する新しいカーネルモードルーチン[**IoIs32bitProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iois32bitprocess)が導入されています。 プロトタイプは次のとおりです。

```cpp
BOOLEAN
  IoIs32bitProcess(
    _In_opt_ PIRP Irp  // NULL for fast I/O call, IRP otherwise
    );
```

**IoIs32bitProcess**は、現在の i/o 要求の発信者が32ビットのユーザーモードアプリケーションである場合に**TRUE**を返します。

次のコードサンプルは、 **IoIs32bitProcess**の使用方法を示しています。

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

 

 





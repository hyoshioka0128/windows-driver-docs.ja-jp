---
title: IoIs32bitProcess を使用して詳細な例
description: IoIs32bitProcess を使用して詳細な例
ms.assetid: bb73d16c-9f9f-41ff-ac0b-8af31c6f55f4
keywords:
- 32 ビットの I/O は、WDK の 64 ビット、IoIs32bitProcess をサポートします。
- IoIs32bitProcess
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae9241bbfd3aa3d0b57fdfde2da9191c19d6ed05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361848"
---
# <a name="extended-example-using-iois32bitprocess"></a>拡張の例: IoIs32bitProcess の使用





次の例への呼び出しを追加することで、64 ビットの 32 ビット ドライバーを変更する方法を示します[ **IoIs32bitProcess**](https://msdn.microsoft.com/library/windows/hardware/ff549372)します。 この例に変更する必要があるドライバー コードの部分のみが表示されるに注意してください。

### <a name="original-driver-code"></a>元のドライバー コード

```cpp
typedef struct _TESTDRV_EVENT_BUFFER {
     HANDLE Handle;
     ULONG Key;
} TESTDRV_EVENT_BUFFER, *PTESTDRV_EVENT_BUFFER;

NTSTATUS
TestdrvFsControl (
    IN PTESTDRV_DEVICE_OBJECT TestdrvDeviceObject,
    IN PIRP Irp
    )
{

    ...

    InputBufferLength = 
        IrpSp->Parameters.FileSystemControl.InputBufferLength;
 

    if (InputBufferLength < sizeof(TESTDRV_EVENT_BUFFER)) {

        DebugTrace(0, Dbg, "System buffer size is too small\n", 0);

        FsRtlCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
        return STATUS_INVALID_PARAMETER;
    }

    Buffer = Irp->AssociatedIrp.SystemBuffer;
 
    // start using the event buffer

    ...

}
```

### <a name="driver-code-with-thunking-support"></a>ドライバーのコードをサンクのサポート

```cpp
typedef struct _TESTDRV_EVENT_BUFFER {
     HANDLE Handle;
     ULONG Key;
} TESTDRV_EVENT_BUFFER, *PTESTDRV_EVENT_BUFFER;

//
// Define a 32-bit thunking structure 
//

 #if defined(_WIN64)
typedef struct _TESTDRV_EVENT_BUFFER32 {
     UINT32 Handle;
     ULONG Key;
} TESTDRV_EVENT_BUFFER32, *PTESTDRV_EVENT_BUFFER32;
#endif

//
// Intercept the input buffer as a 32-bit structure and thunk it to 
 //    64-bit
NTSTATUS
TestdrvFsControl (
    IN PTESTDRV_DEVICE_OBJECT TestdrvDeviceObject,
    IN PIRP Irp
    )
{
    TESTDRV_EVENT_BUFFER LocalBuffer;

    ...

    InputBufferLength  =                             
             IrpSp->Parameters.FileSystemControl.InputBufferLength;
 
#if defined(_WIN64)
    if (IoIs32bitProcess(Irp)) {
        PTESTDRV_EVENT_BUFFER32 Buffer32;

        if (InputBufferLength < sizeof(TESTDRV_EVENT_BUFFER32)) {
            DebugTrace(0, Dbg, "Irp32 : System buffer size is too
                        small\n", 0);

            FsRtlCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
            return STATUS_INVALID_PARAMETER;
        }
        Buffer = &LocalBuffer;
        Buffer32 = Irp->AssociatedIrp.SystemBuffer;
        Buffer->Handle = (HANDLE)Buffer32->Handle;
        Buffer->Key = Buffer32->Key;
    }
    else {
#endif
        if (InputBufferLength < sizeof(TESTDRV_EVENT_BUFFER)) {

            DebugTrace(0, Dbg, "System buffer size is too small\n", 0);

            FsRtlCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
            return STATUS_INVALID_PARAMETER;
        }

        Buffer = Irp->AssociatedIrp.SystemBuffer;
#if defined(_WIN64)
    }
#endif
 
    // start using the Event Buffer

    ...

}
```

 

 





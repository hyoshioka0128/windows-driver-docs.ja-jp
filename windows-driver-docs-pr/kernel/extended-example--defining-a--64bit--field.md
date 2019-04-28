---
title: 「64 ビット」フィールドを定義する拡張例
description: IOCTL 制御コードに「64 ビット」フィールドを追加して 64 ビットの 32 ビット ドライバーを変更する方法を示します。
ms.assetid: 642b67eb-880c-4057-b5de-c89ef8e8601e
keywords:
- 32 ビットの I/O をサポートして WDK 64 ビット、64 ビット フィールドの定義
- 64 ビット フィールドには、WDK のカーネルが定義されています。
- WDK の 64 ビットのビット フィールド
- WDK の 64 ビットの個別の制御コード
- 制御コード WDK 64 ビット
- WDK の 64 ビットのコードをファイル システムの制御
- FSCTL WDK 64 ビット
- I/O 制御コード WDK カーネル、64 ビット ドライバーで 32 ビットの I/O
- Ioctl WDK カーネルでは、64 ビット ドライバーで 32 ビットの I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a449c9a3da97a07b0fbf9b81d3a0aeaccdb9e62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361977"
---
# <a name="extended-example-defining-a-64bit-field"></a>拡張の例: 「64 ビット」フィールドを定義します。





次の例では、IOCTL 制御コードに「64 ビット」フィールドを追加して 64 ビットの 32 ビット ドライバーを変更する方法を示します。 この例に変更する必要があるドライバー コードの部分のみが表示されるに注意してください。

### <a name="original-driver-code"></a>元のドライバー コード

ドライバーの 32 ビット バージョンを次に示します。

### <a name="header-file"></a>ヘッダー ファイル

```cpp
#define REGISTER_FUNCTION 0     // Define the IOCTL function code

#define IOCTL_REGISTER   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)

typedef struct _IOCTL_PARAMETERS {
    PVOID   Addr;
    SIZE_T  Length;
    HANDLE  Handle;
} IOCTL_PARAMETERS, *PIOCTL_PARAMETERS;
```

### <a name="devicecontrol-dispatch-routine"></a>デバイスのディスパッチ ルーチン

```cpp
NTSTATUS
TestdrvDeviceControl(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    PIO_STACK_LOCATION irpSp;
    NTSTATUS status;
    PIOCTL_PARAMETERS params;
    IOCTL_PARAMETERS  LocalParam;
    PIOCTL_PARAMETERS_32 params32;

    //
    // Get a pointer to the current parameters for this request. The
    // information is contained in the current stack location.
    //
    irpSp = IoGetCurrentIrpStackLocation(Irp);
    //
    // Case on the device control code
    //
    switch (irpSp->Parameters.DeviceIoControl.IoControlCode) {
    case IOCTL_REGISTER:
        params = (PIOCTL_PARAMETERS)
            (Irp->AssociatedIrp.SystemBuffer);
        if (irpSp->Parameters.DeviceIoControl.InputBufferLength <
               sizeof(IOCTL_PARAMETERS)) {
            status = STATUS_INVALID_PARAMETER;
        } else {
            RtlCopyMemory(&LocalParam,  params, 
              sizeof(IOCTL_PARAMETERS));
            /* Handle the ioctl here */
            status = STATUS_SUCCESS;
        }
        Irp->IoStatus.Information = 0;
            break;
    //
    // Unrecognized device control request
    //
    default:
        Irp->IoStatus.Information = 0;
        status = STATUS_INVALID_PARAMETER;
        break;
    }
    //
    // If status is pending, mark the IRP pending and start the
    // request in a cancelable state. Otherwise, complete the IRP.
    //
    Irp->IoStatus.Status = status;
 IoCompleteRequest(Irp, IO_NO_INCREMENT);
 return(status);
}
```

### <a name="driver-code-with-thunking-support"></a>ドライバーのコードをサンクのサポート

ドライバーの 64 ビット バージョンを次に示します。

### <a name="header-file"></a>ヘッダー ファイル

```cpp
#define REGISTER_FUNCTION 0     // Define the IOCTL function code

#ifdef  _WIN64
#define CLIENT_64BIT   0x800
#define REGISTER_FUNCTION 0
#define IOCTL_REGISTER   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  CLIENT_64BIT|REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
#else
#define IOCTL_REGISTER   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
#endif

typedef struct _IOCTL_PARAMETERS {
    PVOID   Addr;
    SIZE_T  Length;
    HANDLE  Handle;
} IOCTL_PARAMETERS, *PIOCTL_PARAMETERS;
```

### <a name="devicecontrol-dispatch-routine"></a>デバイスのディスパッチ ルーチン

```cpp
#ifdef _WIN64
#define IOCTL_REGISTER_32   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
 #endif

...

#ifdef _WIN64
typedef struct _IOCTL_PARAMETERS_32 {
    VOID*POINTER_32  Addr;
    INT32            Length;
    VOID*POINTER_32  Handle;
} IOCTL_PARAMETERS_32, *PIOCTL_PARAMETERS_32;
 #endif

...

NTSTATUS
TestdrvDeviceControl(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp
    )
{
    PIO_STACK_LOCATION irpSp;
    NTSTATUS status;
    PIOCTL_PARAMETERS params;
    IOCTL_PARAMETERS  LocalParam;
    PIOCTL_PARAMETERS_32 params32;

    //
    // Get a pointer to the current parameters for this request. The
    // information is contained in the current stack location.
    //
    irpSp = IoGetCurrentIrpStackLocation(Irp);
    //
    // Case on the device control code
    //
    switch (irpSp->Parameters.DeviceIoControl.IoControlCode) {
#ifdef  _WIN64
    case IOCTL_REGISTER_32:
        params32 = (PIOCTL_PARAMETERS_32)
          (Irp->AssociatedIrp.SystemBuffer);
        if (irpSp->Parameters.DeviceIoControl.InputBufferLength < 
            sizeof(IOCTL_PARAMETERS_32)) {
            status = STATUS_INVALID_PARAMETER;
        } else {
            LocalParam.Addr = params32->Addr;
            LocalParam.Handle = params32->Handle;
            LocalParam.Length = params32->Length;
            /* Handle the ioctl here */
            status = STATUS_SUCCESS;
            Irp->IoStatus.Information = 0;
        }
        break;
 #endif
    case IOCTL_REGISTER:
        params = (PIOCTL_PARAMETERS)
            (Irp->AssociatedIrp.SystemBuffer);
        if (irpSp->Parameters.DeviceIoControl.InputBufferLength <
            sizeof(IOCTL_PARAMETERS)) {
            status = STATUS_INVALID_PARAMETER;
        } else {
            RtlCopyMemory(&LocalParam, params, 
                sizeof(IOCTL_PARAMETERS));
            /* Handle the ioctl here */
            status = STATUS_SUCCESS;
        }
        Irp->IoStatus.Information = 0;
        break;
    //
    // Unrecognized device control request
    //
    default:
        Irp->IoStatus.Information = 0;
        status = STATUS_INVALID_PARAMETER;
        break;
    }
    //
    // If status is pending, mark the IRP pending and start the
    // request in a cancelable state. Otherwise, complete the IRP.
    //
    Irp->IoStatus.Status = status;
    IoCompleteRequest(Irp, IO_NO_INCREMENT);
    return(status);
}
```

 

 





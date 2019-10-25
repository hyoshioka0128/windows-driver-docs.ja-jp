---
title: ページング可能なコードの分離
description: ページング可能なコードの分離
ms.assetid: 86189154-606a-4df8-b3a9-040bbaffaa2f
keywords:
- ページング可能ドライバー WDK カーネル、コードの分離
- 分離 (ページング可能コードを)
- スピンロック WDK メモリ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 406319d3b82b11288d89c10ccf7a070090d3769d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827924"
---
# <a name="isolating-pageable-code"></a>ページング可能なコードの分離





スピンロックを使用するルーチンにページングを行うことはできません。 ただし、場合によっては、スピンロックを必要とする操作を、ページング可能なセクションに含まれない別のルーチンで分離することができます。

たとえば、次のようなフラグメントを考えてみます。

```cpp
//  PAGED_CODE(); 
 
KeInitializeEvent( &event, NotificationEvent, FALSE ); 
irp = IoBuildDeviceIoControlRequest( IRP_MJ_DEVICE_CONTROL, 
                                     DeviceObject, 
                                     (PVOID) NULL, 
                                     0, 
                                     (PVOID) NULL, 
                                     0, 
                                     FALSE, 
                                     &event, 
                                     &ioStatus ); 
if (irp) { 
   irpSp = IoGetNextIrpStackLocation( irp ); 
   irpSp->MajorFunction = IRP_MJ_FILE_SYSTEM_CONTROL; 
   irpSp->MinorFunction = IRP_MN_LOAD_FILE_SYSTEM; 
   status = IoCallDriver( DeviceObject, irp ); 
   if (status == STATUS_PENDING) { 
   (VOID) KeWaitForSingleObject( &event, 
                                 Executive, 
                                 KernelMode, 
                                 FALSE, 
                                 (PLARGE_INTEGER) NULL ); 
   } 
} 

SPINLOCKUSE ! 
KeAcquireSpinLock( &IopDatabaseLock, &irql ); 
// Code inside spin lock ...

DeviceObject->ReferenceCount--; 
 
if (!DeviceObject->ReferenceCount && !DeviceObject->AttachedDevice) { 
   //Unload the driver
   .
   .
   . 
} else { 
   KeReleaseSpinLock( &IopDatabaseLock, irql ); 
} 
```

前のルーチンは、スピンロックを参照する数行のコードを別のルーチンに移動することによって、ページング可能にする (約160バイトを節約する) ことができます。

さらに、 *Wait*パラメーターが**TRUE**に設定されている[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)や[**KeReleaseSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore)などの**Ke * Xxx*** サポートルーチンを呼び出す場合は、ドライバーコードがページング可能としてマークされていないことに注意してください。 このような呼び出しでは、ディスパッチ\_レベルで IRQL が返されます。

 

 





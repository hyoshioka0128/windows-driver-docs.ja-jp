---
title: ページング可能なコードの分離
description: ページング可能なコードの分離
ms.assetid: 86189154-606a-4df8-b3a9-040bbaffaa2f
keywords:
- ページング可能なドライバー WDK カーネル、コードの分離
- ページング可能なコードの分離
- スピン ロック WDK メモリ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aeac616d22df883b0ba9a919bd5c3b0e0dc8587
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381391"
---
# <a name="isolating-pageable-code"></a>ページング可能なコードの分離





スピン ロックを使用するルーチンがページングされることはできません。 ただし、場合によっては、ページング可能なセクションに含まれていないのは別のルーチンでスピン ロックを必要とする操作を分離できます。

たとえば、次のフラグメントを考えてみます。

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

上記のルーチンを持たせてページング可能な (約 160 バイトの保存)、スピン ロックを別のルーチンに参照するわずか数行のコードを移動することによって。

さらに、覚えてドライバー コードする必要がありますいないマークすることと、いずれかを呼び出す場合ページング可能な**Ke * Xxx*** などのルーチンのサポート[ **KeReleaseMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553140)または[ **KeReleaseSemaphore**](https://msdn.microsoft.com/library/windows/hardware/ff553143)、これで、*待機*パラメーターを設定する**TRUE**。 このような呼び出しがディスパッチで IRQL を返します\_レベル。

 

 





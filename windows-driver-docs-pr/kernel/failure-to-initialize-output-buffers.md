---
title: 出力バッファーの初期化失敗
description: 出力バッファーの初期化失敗
ms.assetid: 8c038a94-8506-44e3-ac7f-82b58d791124
keywords:
- 出力バッファーの WDK カーネル
- 出力バッファーを初期化しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94dcc2403f1d6ec633a20f9fd23dcbd874efb489
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359997"
---
# <a name="failure-to-initialize-output-buffers"></a>出力バッファーの初期化失敗





ドライバーは、呼び出し元に返す前に 0 で、すべての出力バッファーを初期化する必要があります。 バッファーの初期化に失敗すると、初期化されていないバイトにガベージ データがあります。

次の例では、ドライバーは、ガベージ (未使用のバイト単位) を返します。

```cpp
   case IOCTL_GET_NAME: {
      ...
      ...
      outputBufferLength = 
         ioStack->Parameters.DeviceIoControl.OutputBufferLength;
      outputBuffer = (PGET_NAME) Irp->AssociatedIrp.SystemBuffer;
 
      if (outputBufferLength >= sizeof(GET_NAME)) {
         length = outputBufferLength - sizeof(GET_NAME);
 
         ntStatus = IoGetDeviceProperty(
                        DeviceExtension->PhysicalDeviceObject,
                        DevicePropertyDriverKeyName,
                        length,
                        outputBuffer->DriverKeyName,
                        &length);

         outputBuffer->ActualLength =
                        length + sizeof(GET_NAME);

         Irp->IoStatus.Information = outputBufferLength;
 
      } else {
         ntStatus = STATUS_BUFFER_TOO_SMALL;
      }
```

設定**IoStatus.Information**出力バッファー サイズによって、出力、呼び出し元に返されるバッファーは全体にします。 I/O マネージャーが入力バッファーのサイズを超えたデータを初期化できません: バッファー内の要求の入力と出力バッファーが重複します。 システム ルーチンをサポートするため、 [ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)書き込みませんバッファー全体については、この IOCTL では、初期化されていないデータを呼び出し元に返します。

一部のドライバーを使用して、**情報**I/O 要求についての詳細情報を提供するコードを返すフィールド。 これを行うには、前にこのようなドライバーが確実に IRP フラグを確認します。 その IRP\_入力\_操作が設定されていません。 このフラグが設定されていない場合、IOCTL または FSCTL が出力バッファーでは、そのため、**情報**フィールドは、バッファー サイズを指定しない必要があります。 この場合です。 ドライバーは安全に使用できます、**情報**フィールドを独自のコードを返します。

 

 





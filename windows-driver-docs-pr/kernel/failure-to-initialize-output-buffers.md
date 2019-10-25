---
title: 出力バッファーを初期化できませんでした
description: 出力バッファーを初期化できませんでした
ms.assetid: 8c038a94-8506-44e3-ac7f-82b58d791124
keywords:
- 出力バッファー WDK カーネル
- 初期化 (出力バッファーを)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43127eba479bb89f2ad4855694f0bde38e4dab70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838699"
---
# <a name="failure-to-initialize-output-buffers"></a>出力バッファーを初期化できませんでした





ドライバーは、呼び出し元に返す前に、すべての出力バッファーをゼロで初期化する必要があります。 バッファーの初期化に失敗すると、初期化されていないバイトでガベージデータが発生する可能性があります。

次の例では、ドライバーが使用されていないバイトでガベージを返します。

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

**Iostatus. 情報**を出力バッファーサイズに設定すると、出力バッファー全体が呼び出し元に返されます。 I/o マネージャーは、入力バッファーのサイズを超えてデータを初期化するのではなく、バッファー内の要求に対して入力バッファーと出力バッファーが重複します。 システムサポートルーチン[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)はバッファー全体を書き込まないため、この IOCTL は初期化されていないデータを呼び出し元に返します。

一部のドライバーでは、**情報**フィールドを使用して、i/o 要求に関する追加情報を提供するコードを返します。 その前に、このようなドライバーでは、irp フラグをチェックして、IRP\_入力\_操作が設定されていないことを確認する必要があります。 このフラグが設定されていない場合、IOCTL または FSCTL には出力バッファーがないため、**情報**フィールドにバッファーサイズを指定する必要はありません。 この場合はです。 ドライバーは、**情報**フィールドを安全に使用して、独自のコードを返すことができます。

 

 





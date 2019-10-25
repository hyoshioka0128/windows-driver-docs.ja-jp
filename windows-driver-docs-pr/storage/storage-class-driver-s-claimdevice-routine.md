---
title: 記憶域クラス ドライバーの ClaimDevice ルーチン
description: 記憶域クラス ドライバーの ClaimDevice ルーチン
ms.assetid: 175b9be6-34a5-4d20-970c-aa9a6880c242
keywords:
- ClaimDevice
- 記憶デバイスの要求
- クエリ-プロパティは WDK ストレージを要求します
- 構成情報 WDk ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af0e257b64ba7707630f4f5c92bbf9ecebd090b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844749"
---
# <a name="storage-class-drivers-claimdevice-routine"></a>記憶域クラス ドライバーの ClaimDevice ルーチン


## <span id="ddk_storage_class_drivers_claimdevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_CLAIMDEVICE_ROUTINE_KG"></span>


ストレージデバイスを要求する*Claimdevice*ルーチンは、通常、[ストレージクラスドライバーの AddDevice ルーチン](storage-class-driver-s-adddevice-routine.md)から呼び出されます。

ストレージデバイスを要求するために、クラスドライバーは、 *AddDevice*呼び出しでクラスドライバーに渡された PDO を使用して[**IoGetAttachedDeviceReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)を呼び出すことによってデバイスオブジェクトへの参照を取得し、次から内部の*claimdevice*ルーチンを呼び出します。*AddDevice*ルーチン。または、同じ機能をインラインで実装します。 *Claimdevice*ルーチンは、**関数**値 SRB\_関数\_要求\_デバイスを使用して SRB を設定し、クラスドライバーの**IoGetAttachedDeviceReference**への呼び出しによって返されるデバイスオブジェクトに送信します。

*Claimdevice*ルーチンは、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を使用して IRP を割り当てます。 i/o 制御コード\_\_IOCTL を使用してポートドライバーの i/o スタック位置を設定し\_NONE と SRB**へのポインターを実行します。Srb**。 また、 *Claimdevice*は、IRP の完了を待機できるように**keinitializeevent**を使用してイベントオブジェクトを設定する必要があります。 次に、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、IRP を次の下位のドライバーに送信します。

IRP が完了すると、 *Claimdevice*は**IoGetAttachedDeviceReference**から返されたデバイスオブジェクトへの参照を解放する必要があります。

*Claimdevice*ルーチンは、クラスドライバーの*removedevice*ルーチンから呼び出されるルーチンとして、またはドライバーがデバイスの要求に成功してもデバイスオブジェクトを作成できない場合は、 *AddDevice*からの2つの職務を提供できます。 このような場合、 *Claimdevice*は、**関数**値 SRB\_関数\_リリース\_デバイスに対して、SRB を送信します。

 

 





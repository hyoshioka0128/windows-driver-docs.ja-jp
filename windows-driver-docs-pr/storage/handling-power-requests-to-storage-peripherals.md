---
title: 記憶域周辺機器への電源要求の処理
description: 記憶域周辺機器への電源要求の処理
ms.assetid: 3cc7b885-27ad-4384-aeec-4d76f9ad4f1c
keywords:
- 周辺機器 WDK ストレージ、電源要求
- ストレージ周辺機器 WDK、電源要求
- WDK ストレージに対する電力要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b62cf17e23342fb413208bff02cde295f664ba8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826292"
---
# <a name="handling-power-requests-to-storage-peripherals"></a>記憶域周辺機器への電源要求の処理


## <span id="ddk_handling_power_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_POWER_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


ストレージクラスドライバーは、電源要求を処理するためのデバイス固有のコマンドを発行する役割を担います。 最も一般的なストレージクラスのドライバーは、次のとおりです。

-   クエリ-電源要求に応答してデバイスに i/o をブロックします (IRP\_MJ は、 [**irp\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)\_パワー)。このような i/o を処理すると、ドライバーが適切な量のセット電源要求を実行できなくなる可能性があります。時間

-   Set-パワー要求に応答してデバイスの電源状態を設定します (IRP\_MJ\_、Irp\_を使用した電源[ **\_設定\_電力**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power))

-   デバイスの電源をオンにするためのセットパワー要求に応じて、デバイスに i/o を再起動します。

-   電源要求を次の下位のドライバーに転送します。

ドライバーは、電源要求を送信するために、 **IoCallDriver**ではなく[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)と[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を呼び出す必要があることに注意してください。

ストレージクラスドライバーに[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが含まれていない場合は、デバイスの電源状態を設定する前に、ストレージポートドライバーの LU 固有のキュー (IRP\_MJ\_SCSI で SRB\_関数\_ロック\_キュー) をロックする必要があります。電源操作 (いくつかの手順が含まれる場合があります) が完了するまで、同期されていない操作をブロックします。 電源操作を処理するために発行されたすべての SRBs は、SRB\_フラグ\_設定して、ロックされた\_キュー\_バイパスし、ポートドライバーに確実に到着するようにする必要があります。 ドライバーが電源状態の設定を完了したら、キューのロックを解除する必要があります (IRP\_MJ\_SCSI は、SRB\_関数\_ロック解除\_QUEUE および SRB\_フラグ\_\_ロックされている\_キューをバイパス)ポートドライバーは、電源が投入された後、デバイスにキューに入っている Irp の送信を再開できます。

ストレージクラスドライバーに*StartIo*ルーチンが含まれている場合、そのルーチンは同期を処理するので、クラスドライバーはポートドライバーの LU 固有のキューを明示的にロックおよびロック解除する必要がありません。

クラスドライバーは、別のドライバーによってロックされているキューをバイパスしようとすることはできません。

 

 





---
title: ATA ポート ドライバーのキュー管理
description: ATA ポート ドライバーのキュー管理
ms.assetid: feba86a6-2b89-41c9-9b14-b76c2522a332
keywords:
- ATA ポートドライバー WDK、キュー
- WDK ATA ポートドライバーをキューに置いてください
- デバイスキュー WDK ATA ポートドライバー
- LUN キュー WDK ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f53e19e772ccf720f84c4eea112a6eecc4cc147a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845105"
---
# <a name="ata-port-drivers-queue-management"></a>ATA ポート ドライバーのキュー管理


## <span id="ddk_ata_port_drivers_queue_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_QUEUE_MANAGEMENT_KG"></span>


**メモ**ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。


ATA ポートドライバーは、ミニポートドライバーによって公開されている論理ユニット番号 (LUN) ごとにデバイスキューを保持し、IDE コントローラーで有効になっているチャネルごとに個別のキューを保持します。 これらのキューは、ミニポートドライバーへの要求のフローを制御するために連携します。

次の図は、ポートドライバーの LUN キューからチャネルキューへの要求のフローを示しています。

![ata デバイスキューとチャネルキュー](images/ataqueues.png)

ATA ポートドライバーでは i/o のプッシュモデルが使用されるため、ATA ポートドライバーはミニポートドライバーが次のパケットをミニポートドライバーに転送する前に入力を要求するのを待機しません。 ATA ポートドライバーで使用される i/o モデルの詳細については、「 [Ata ポート I/o モデル](ata-port-i-o-model.md)」を参照してください。

それに*もかかわらず*、ATA ポートドライバーでは、ミニポートドライバーにプッシュダウンされる要求の数が制限されます。 要求の数は、ミニポートドライバーが[**IDE\_チャネル\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/ns-irb-_ide_channel_configuration)構造の**NumberOfOverlappedRequests**メンバーに割り当てる値です。 ATA ポートドライバーは、特定のチャネルのミニポートドライバーに転送された未完了の "重複" 要求の数を保持します。 この数値が**NumberOfOverlappedRequests**の値を超えると、ATA ポートドライバーはミニポートドライバーへの新しい要求の受け渡しを停止します。 ATA ポートドライバーは、すべての新しい要求をキューに保持し、ミニポートドライバーがいくつかの要求を完了するまで待機します。 未処理の要求の数が**NumberOfOverlappedRequests**の値を下回ると、ポートドライバーはミニポートドライバーへの要求の送信を再開します。

ATA ミニポートドライバーは、 [**AtaPortDeviceBusy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportdevicebusy)ルーチンと[**AtaPortDeviceReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportdeviceready)ルーチンを呼び出すことによって、ポートドライバーから受信する要求のフローを制御することもできます。

 

 



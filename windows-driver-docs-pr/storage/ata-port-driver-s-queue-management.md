---
title: ATA ポート ドライバーのキュー管理
description: ATA ポート ドライバーのキュー管理
ms.assetid: feba86a6-2b89-41c9-9b14-b76c2522a332
keywords:
- ATA ポート ドライバー WDK、キュー
- キューの WDK ATA ポート ドライバー
- デバイスのキューの WDK ATA ポート ドライバー
- LUN キュー WDK ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edba5c8a75922c3098bf4d9f11820ae5b424264e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574519"
---
# <a name="ata-port-drivers-queue-management"></a>ATA ポート ドライバーのキュー管理


## <span id="ddk_ata_port_drivers_queue_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_QUEUE_MANAGEMENT_KG"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


ATA ポート ドライバーには、デバイスのキュー、ミニポート ドライバーによって公開される各論理ユニット番号 (LUN) の IDE コント ローラーで有効になっている各チャネルに対して別のキューが維持されます。 これらのキューが連携して、ミニポート ドライバーへの要求のフローを制御します。

次の図は、ポート ドライバーの LUN のキューからチャネルのキューに要求のフローを示しています。

![ata のデバイスとチャネルのキュー](images/ataqueues.png)

ATA ポート ドライバーは、I/O のプッシュ モデルを使用しているために、ATA ポート ドライバーはミニポート ドライバーのミニポート ドライバーには、次のパケットを転送する前に、入力を要求を待機しません。 ATA のポートのドライバーを使用する I/O モデルについては、[ATA ポート I/O モデル](ata-port-i-o-model.md)を参照してください。

それにもかかわらず、ATA ポート ドライバー*は*ミニポート ドライバーにプッシュ ダウンの要求の数を制限します。 要求の数は、ミニポート ドライバーに割り当てられている値、 **NumberOfOverlappedRequests**のメンバー、 [ **IDE\_チャネル\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff559029)構造体。 ATA ポート ドライバーでは、その特定のチャネルのミニポート ドライバーに転送が未完了の「重複」要求の数のカウントを保持します。 この数の値を超えた場合**NumberOfOverlappedRequests**、ミニポート ドライバーに新しい要求を渡す ATA ポート ドライバーを停止します。 ATA ポート ドライバーは、キューにすべての新しい要求を保持し、ミニポート ドライバーが一部の要求を完了するまで待機します。 未処理の要求の数の値を下回る後**NumberOfOverlappedRequests**、ミニポート ドライバーに要求を送信ポートのドライバーを再開します。

ATA のミニポート ドライバーではポート ドライバーから呼び出すことで受信した要求のフローを制御できますも、 [ **AtaPortDeviceBusy** ](https://msdn.microsoft.com/library/windows/hardware/ff550155)と[ **AtaPortDeviceReady**](https://msdn.microsoft.com/library/windows/hardware/ff550157)ルーチン。

 

 



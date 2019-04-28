---
title: ATA ポート ドライバー
description: ATA ポート ドライバー
ms.assetid: c7b9d794-a8cb-4bdd-bb93-bff473ea26a7
keywords:
- 記憶域ポート ドライバー WDK、ATA ポート ドライバー
- ATA ポート ドライバー WDK
- ATA ポート ドライバー WDK、ATA ポート ドライバーについて
- IDE コント ローラーの WDK ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e644b187f6c5be9626e852907f220adedc2e230d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380126"
---
# <a name="ata-port-driver"></a>ATA ポート ドライバー


## <span id="ddk_ata_port_driver_kg"></span><span id="DDK_ATA_PORT_DRIVER_KG"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


加え、 [SCSI ポート ドライバー](scsi-port-driver.md)と[Storport ドライバー](storport-driver.md)、Windows Vista および Windows オペレーティング システムの以降のバージョンの提供、ATA ポート ドライバー (*Ataport.sys*)、IDE コント ローラーで使用するために特に適したストレージ ポート ドライバー。

ATA ポート ドライバーと他のシステムが指定したストレージ ポート ドライバーとの間の最も重要な違いは、ATA ポート ドライバーは、他のドライバーとの通信に使用するプロトコルです。 他のすべてのシステムが指定したストレージ ポート ドライバーは、ミニポート ドライバーと記憶域クラス ドライバーより高度なドライバーは、両方の通信に SCSI 要求のブロック (される Srb) を使用します。 ATA ポート ドライバーでは、される Srb を使用してより高度なドライバーのみと通信します。 ATA のポートがによって定義されている IDE 要求ブロック (IRB) と呼ばれるパケットを使用するには、ミニポート ドライバーの通信を[ **IDE\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559140)構造体。 IRBs は設計される Srb ATA デバイスの特性によりします。

ATA ポート ドライバーと他のシステム提供の記憶装置ドライバーにはもう 1 つの違いは、SCSI 標準で定義されている特定の要件から ATA ミニポート ドライバーを ATA ポート ドライバーが明らかにならないようにします。 たとえば、ATA ポート ドライバーは、ATA コマンドを使用して、ATA のミニポート ドライバーからと同等の SCSI センス データを収集、SCSI センス データ形式に準拠し、SCSI センス データの場合と同様より高度なドライバーにデータを渡すように、データを変換します。 そのため、ATA のミニポート ドライバーは、SCSI センス データの上位レベルのドライバーからの要求に直接応答はありません。

ATA のミニポート ドライバー インターフェイスには、SCSI ポート ドライバー インターフェイスによく似ています。 そのため、SCSI ミニポート ドライバーを既に作成した場合、ATA のミニポート ドライバーを作成する方法を簡単に習得はずです。 Serial ATA (SATA) など、現在の ATA/ATAPI テクノロジ用のドライバーより高いパフォーマンス Storport ミニポート インターフェイスを使用する必要があります。

ATA ポート ドライバーとは、オペレーティング システムは、既定の ATA ミニポート ドライバーと既定のコント ローラー ミニドライバーを提供します。 ほとんどのコント ローラーのハードウェアには、システム提供の既定のドライバーが動作し、可能な限り、既定のミニドライバーを使用することを強くお勧めします。

 

 



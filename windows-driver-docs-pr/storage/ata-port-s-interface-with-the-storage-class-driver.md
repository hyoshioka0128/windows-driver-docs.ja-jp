---
title: ATA ポートと記憶域クラス ドライバーとのインターフェイス
description: ATA ポートと記憶域クラス ドライバーとのインターフェイス
ms.assetid: 6b22bbb1-f14e-48d9-a00c-c7eae79a078f
keywords:
- ATA ポートドライバー WDK、ストレージクラスドライバー
- ストレージクラスドライバー WDK、ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9304e2cecdecd69d1e55b95ed57704455ffb54b
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606492"
---
# <a name="ata-ports-interface-with-the-storage-class-driver"></a>ATA ポートと記憶域クラス ドライバーとのインターフェイス

> [!NOTE]
> ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver-overview)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。

ATA ポートドライバー、SCSI ポートドライバー、および Storport ドライバーはすべて、SRBs を使用して、記憶域クラスドライバーなどの上位レベルのドライバーと通信します。 ストレージクラスとストレージポートドライバーの間のインターフェイスの詳細については、「 [SCSI ポートのインターフェイスと記憶域クラスドライバー](scsi-port-s-srb-interface-with-the-storage-class-driver.md)」を参照してください。

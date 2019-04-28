---
title: ATA ポートと記憶域クラス ドライバーとのインターフェイス
description: ATA ポートと記憶域クラス ドライバーとのインターフェイス
ms.assetid: 6b22bbb1-f14e-48d9-a00c-c7eae79a078f
keywords:
- ATA ポート ドライバー WDK、記憶域クラス ドライバー
- 記憶域クラス ドライバー WDK、ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96bf6bc0dd2802eae8abed43178625c249edc8b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380125"
---
# <a name="ata-ports-interface-with-the-storage-class-driver"></a>ATA ポートと記憶域クラス ドライバーとのインターフェイス


## <span id="ddk_ata_ports_interface_with_the_storage_class_driver_kg"></span><span id="DDK_ATA_PORTS_INTERFACE_WITH_THE_STORAGE_CLASS_DRIVER_KG"></span>

**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。



ATA ポート ドライバー、SCSI ポート ドライバー、および Storport ドライバーされる Srb を記憶域クラス ドライバーなどのより高度なドライバーとの通信に使用します。 ストレージ クラスとストレージ ポート ドライバーとの間のインターフェイスの詳細については、次を参照してください。[ストレージ クラス ドライバーを使用した SCSI ポートのインターフェイス](scsi-port-s-interface-with-the-storage-class-driver.md)します。

 

 



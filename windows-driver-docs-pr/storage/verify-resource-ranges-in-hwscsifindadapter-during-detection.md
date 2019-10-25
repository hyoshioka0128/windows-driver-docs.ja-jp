---
title: HwScsiFindAdapter での検出時のリソース範囲の確認
description: HwScsiFindAdapter での検出時のリソース範囲の確認
ms.assetid: 2909aac2-714e-4353-8006-06cf68e4dfc8
keywords:
- SCSI ミニポートドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- WDK SCSI のプラグアンドプレイ
- SCSI ミニポートドライバーの変換
- リソース範囲 WDK SCSI
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d7afbb76855329bcbeb22cb8c2635b8fd567a13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845585"
---
# <a name="verify-resource-ranges-in-hwscsifindadapter-during-detection"></a>HwScsiFindAdapter での検出時のリソース範囲の確認


## <span id="ddk_verify_resource_ranges_in_hwscsifindadapter_during_detection_kg"></span><span id="DDK_VERIFY_RESOURCE_RANGES_IN_HWSCSIFINDADAPTER_DURING_DETECTION_KG"></span>


通常、プラグアンドプレイでは、ドライバーによるデバイスの検出は不要ですが、ポートドライバーは、非列挙型バス上のデバイスを検出するためにプラグアンドプレイミニポートドライバーの[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンを呼び出す場合があります。 この操作は Microsoft Windows NT 4.0 での検出に似ていますが、ミニポートドライバーは、別のデバイスで使用されている可能性がある範囲で動作しないように注意する必要があります。

ミニポートドライバーが指定した範囲が安全に使用できることを確認するため、 [**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase)を呼び出す前に[**ScsiPortValidateRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportvalidaterange)を呼び出す必要があります。 **ScsiPortGetDeviceBase**が失敗し、 **NULL**ポインターが返されるように、ミニポートドライバーを準備する必要があります。 また、ミニポートドライバーでは、アドレス0から始まるマッピングメモリを回避する必要があります。これにより、一部のシステムで**ScsiPortGetDeviceBase**の障害を検出することができなくなります。

 

 





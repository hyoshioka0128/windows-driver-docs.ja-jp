---
title: HwScsiFindAdapter での検出時のリソース範囲の確認
description: HwScsiFindAdapter での検出時のリソース範囲の確認
ms.assetid: 2909aac2-714e-4353-8006-06cf68e4dfc8
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- SCSI ミニポート ドライバーに変換します。
- リソースの範囲は WDK SCSI
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b4aec63e5b624c3e013230edbb5f6ad2a6d26d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386789"
---
# <a name="verify-resource-ranges-in-hwscsifindadapter-during-detection"></a>HwScsiFindAdapter での検出時のリソース範囲の確認


## <span id="ddk_verify_resource_ranges_in_hwscsifindadapter_during_detection_kg"></span><span id="DDK_VERIFY_RESOURCE_RANGES_IN_HWSCSIFINDADAPTER_DURING_DETECTION_KG"></span>


ドライバーによってデバイスの検出は、プラグ アンド プレイの下で通常必要ありませんが、ポートのドライバーがプラグ アンド プレイのミニポート ドライバーを呼び出すことができます[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンでデバイスを検出するために、nonenumerable バスです。 この操作は、Microsoft Windows NT 4.0 での検出と似ていますが、ミニポート ドライバーする必要があることに注意操作範囲を別のデバイスで使用されている可能性があります。

ミニポート ドライバーを呼び出す必要があります[ **ScsiPortValidateRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportvalidaterange)呼び出す前に[ **ScsiPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)ことを確認する、ミニポート ドライバーが指定した範囲を安全に使用します。 ミニポート ドライバーに対応する必要があります**ScsiPortGetDeviceBase**に失敗し、返す、 **NULL**ポインター。 ミニポート ドライバーは、アドレス ゼロで始まるの障害を検出するが不可能マッピング メモリを避ける必要がありますも**ScsiPortGetDeviceBase**一部のシステムです。

 

 





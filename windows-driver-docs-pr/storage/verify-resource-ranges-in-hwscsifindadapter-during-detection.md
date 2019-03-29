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
ms.openlocfilehash: 9c1525edd5204f78dee4eb2b4cb8f6d0f2e24da8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579106"
---
# <a name="verify-resource-ranges-in-hwscsifindadapter-during-detection"></a>HwScsiFindAdapter での検出時のリソース範囲の確認


## <span id="ddk_verify_resource_ranges_in_hwscsifindadapter_during_detection_kg"></span><span id="DDK_VERIFY_RESOURCE_RANGES_IN_HWSCSIFINDADAPTER_DURING_DETECTION_KG"></span>


ドライバーによってデバイスの検出は、プラグ アンド プレイの下で通常必要ありませんが、ポートのドライバーがプラグ アンド プレイのミニポート ドライバーを呼び出すことができます[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)ルーチンでデバイスを検出するために、nonenumerable バスです。 この操作は、Microsoft Windows NT 4.0 での検出と似ていますが、ミニポート ドライバーする必要があることに注意操作範囲を別のデバイスで使用されている可能性があります。

ミニポート ドライバーを呼び出す必要があります[ **ScsiPortValidateRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564761)呼び出す前に[ **ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629)ことを確認する、ミニポート ドライバーが指定した範囲を安全に使用します。 ミニポート ドライバーに対応する必要があります**ScsiPortGetDeviceBase**に失敗し、返す、 **NULL**ポインター。 ミニポート ドライバーは、アドレス ゼロで始まるの障害を検出するが不可能マッピング メモリを避ける必要がありますも**ScsiPortGetDeviceBase**一部のシステムです。

 

 





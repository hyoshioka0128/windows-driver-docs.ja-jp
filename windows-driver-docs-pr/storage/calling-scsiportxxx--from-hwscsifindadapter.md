---
title: HwScsiFindAdapter から ScsiPortXxx の呼び出し
description: HwScsiFindAdapter から ScsiPortXxx の呼び出し
ms.assetid: 17cfca31-ff93-4882-872c-ab8af6cdc3cf
keywords:
- HwScsiFindAdapter
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiFindAdapter
- WDK ストレージ ScsiPortXxx ルーチンを呼び出す
- ScsiPortXxx 呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f3251caebd4ac64a2cec2c3daa4e877bbc3ee6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579442"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>HwScsiFindAdapter から ScsiPortXxx の呼び出し


## <span id="ddk_calling_scsiportxxx_from_hwscsifindadapter_kg"></span><span id="DDK_CALLING_SCSIPORTXXX_FROM_HWSCSIFINDADAPTER_KG"></span>


特定 **ScsiPort * * * Xxx*ルーチンを呼び出すことができる*のみ*ミニポート ドライバーから*HwScsiFindAdapter* routine(s)、具体的には、次。

-   [**ScsiPortValidateRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564761)ことミニポート ドライバーによって提供される、バスの相対にアクセスできる範囲いないは既に要求されて、レジストリにそのデバイスに対して別のドライバーを確認します。

-   [**ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629) HBA ドライバーが呼び出すことによって、HBA との通信に使用できるシステムによって割り当てられた論理アドレス範囲のため (バスの相対)「物理」のアドレス範囲をマップする、**ScsiPortRead * * * Xxx*と **ScsiPortWrite * * * Xxx*マップでの論理ルーチンのアドレス範囲します。

-   [**ScsiPortFreeDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564623)場合は、このようなマップされた範囲を解放する*HwScsiFindAdapter*ポートによって示される、特定の I/O バスでサポートできる HBA が見つからない\_構成\_情報**SystemIoBusNumber**値。

-   [**ScsiPortGetUncachedExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff564639)システム バス マスター HBA の間で共有 DMA バッファーを割り当てられません。

これら 4 つのルーチンに加え、ミニポート ドライバーからのみ呼び出すことは 1 つのルーチンが*HwScsiFindAdapter*ルーチン*または*から*HwScsiAdapterControl*コントロールの種類が場合**ScsiSetRunningConfig**:

-   [**ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)バスを取得する\_データ\_bus 相対デバイス メモリ (アクセス) の範囲、割り込みベクター IRQL などの種類に固有の構成情報と DMA チャネルまたはポート。

これらの詳細については **ScsiPort * * * Xxx*ルーチンを参照してください[SCSI ポート ライブラリ ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff565375)します。

 

 





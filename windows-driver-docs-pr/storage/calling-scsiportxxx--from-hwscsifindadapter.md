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
ms.openlocfilehash: 33db0ecffeea18322961635cf2362d380fa32965
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368354"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>HwScsiFindAdapter から ScsiPortXxx の呼び出し


## <span id="ddk_calling_scsiportxxx_from_hwscsifindadapter_kg"></span><span id="DDK_CALLING_SCSIPORTXXX_FROM_HWSCSIFINDADAPTER_KG"></span>


特定 **ScsiPort * * * Xxx*ルーチンを呼び出すことができる*のみ*ミニポート ドライバーから*HwScsiFindAdapter* routine(s)、具体的には、次。

-   [**ScsiPortValidateRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportvalidaterange)ことミニポート ドライバーによって提供される、バスの相対にアクセスできる範囲いないは既に要求されて、レジストリにそのデバイスに対して別のドライバーを確認します。

-   [**ScsiPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase) HBA ドライバーが呼び出すことによって、HBA との通信に使用できるシステムによって割り当てられた論理アドレス範囲のため (バスの相対)「物理」のアドレス範囲をマップする、**ScsiPortRead * * * Xxx*と **ScsiPortWrite * * * Xxx*マップでの論理ルーチンのアドレス範囲します。

-   [**ScsiPortFreeDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportfreedevicebase)場合は、このようなマップされた範囲を解放する*HwScsiFindAdapter*ポートによって示される、特定の I/O バスでサポートできる HBA が見つからない\_構成\_情報**SystemIoBusNumber**値。

-   [**ScsiPortGetUncachedExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetuncachedextension)システム バス マスター HBA の間で共有 DMA バッファーを割り当てられません。

これら 4 つのルーチンに加え、ミニポート ドライバーからのみ呼び出すことは 1 つのルーチンが*HwScsiFindAdapter*ルーチン*または*から*HwScsiAdapterControl*コントロールの種類が場合**ScsiSetRunningConfig**:

-   [**ScsiPortGetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)バスを取得する\_データ\_bus 相対デバイス メモリ (アクセス) の範囲、割り込みベクター IRQL などの種類に固有の構成情報と DMA チャネルまたはポート。

これらの詳細については **ScsiPort * * * Xxx*ルーチンを参照してください[SCSI ポート ライブラリ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 





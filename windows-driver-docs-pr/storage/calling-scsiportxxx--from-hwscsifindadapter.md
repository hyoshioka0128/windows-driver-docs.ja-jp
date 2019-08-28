---
title: HwScsiFindAdapter から ScsiPortXxx を呼び出しています
description: HwScsiFindAdapter から ScsiPortXxx を呼び出しています
ms.assetid: 17cfca31-ff93-4882-872c-ab8af6cdc3cf
keywords:
- HwScsiFindAdapter
- SCSI ミニポートドライバー WDK 記憶域、HwScsiFindAdapter
- ScsiPortXxx ルーチン WDK storage の呼び出し
- ScsiPortXxx 呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 387e58d30a38d84473cf02e7ceaa01aef3a1143c
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063906"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>HwScsiFindAdapter から ScsiPortXxx を呼び出しています


## <span id="ddk_calling_scsiportxxx_from_hwscsifindadapter_kg"></span><span id="DDK_CALLING_SCSIPORTXXX_FROM_HWSCSIFINDADAPTER_KG"></span>


特定の**ScsiPort**_Xxx_ルーチンは、特に次のようなミニポートドライバーの*HwScsiFindAdapter*ルーチンから*のみ*呼び出すことができます。

-   [**ScsiPortValidateRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportvalidaterange)は、ミニポートドライバーが提供したバス相対アクセス範囲が、そのデバイスの別のドライバーによってレジストリにまだ要求されていないことを確認します。

-   [**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)は、 **ScsiPortRead**_Xxx_を**呼び出して、ドライバーが hba との通信に使用できるシステムによって割り当てられた論理アドレス範囲に、hba の (バス相対) "物理" アドレス範囲をマップします。ScsiPortWrite**_Xxx_ルーチンは、マップされた論理範囲アドレスを使用します。

-   [**ScsiPortFreeDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportfreedevicebase)は、ポート\_構成\_情報に示されているように、特定の i/o バスでサポートできる HBA を*HwScsiFindAdapter*が検出できない場合に、このようなマップされた範囲を解放します。数値.

-   [**ScsiPortGetUncachedExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetuncachedextension)は、システムとバスマスタ HBA の間で共有される DMA バッファーを割り当てることができます。

これらの4つのルーチンに加えて、ミニポートドライバーの*HwScsiFindAdapter*ルーチンからのみ呼び出すことができるルーチンと、コントロールの種類が**ScsiSetRunningConfig**の場合は*HwScsiAdapterControl*から呼び出すことができるルーチンが1つあります。

-   バスの相対デバイス\_メモリ\_(アクセス) 範囲、割り込みベクターまたは IRQL、DMA チャネルまたはポートなど、バスデータ型に固有の構成情報を取得する[**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata) 。

これらの**ScsiPort**_Xxx_ルーチンの詳細については、「 [SCSI ポートライブラリルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)」を参照してください。

 

 





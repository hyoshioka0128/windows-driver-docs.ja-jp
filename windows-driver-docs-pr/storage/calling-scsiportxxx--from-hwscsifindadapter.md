---
title: HwScsiFindAdapter から ScsiPortXxx を呼び出しています
description: HwScsiFindAdapter から ScsiPortXxx を呼び出しています
ms.assetid: 17cfca31-ff93-4882-872c-ab8af6cdc3cf
keywords:
- HwScsiFindAdapter
- SCSI ミニポートドライバー WDK 記憶域、HwScsiFindAdapter
- ScsiPortXxx ルーチン WDK storage の呼び出し
- ScsiPortXxx 呼び出し
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7508b77a28985d81478ef277dd627e34cbf9df62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844509"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>HwScsiFindAdapter から ScsiPortXxx を呼び出しています

特定の**ScsiPort**_Xxx_ルーチンは、特に次のようなミニポートドライバーの*HwScsiFindAdapter*ルーチンから*のみ*呼び出すことができます。

- [**ScsiPortValidateRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportvalidaterange)は、ミニポートドライバーが提供したバス相対アクセス範囲が、そのデバイスの別のドライバーによってレジストリにまだ要求されていないことを確認します。

- [**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase)は、 **ScsiPortRead**_Xxx_を**呼び出して、ドライバーが hba との通信に使用できるシステムによって割り当てられた論理アドレス範囲に、hba の (バス相対) "物理" アドレス範囲をマップします。ScsiPortWrite**_Xxx_ルーチンは、マップされた論理範囲アドレスを使用します。

- [**ScsiPortFreeDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportfreedevicebase)は、 *HwScsiFindAdapter*が特定の i/o バスでサポートできる HBA を検出できない場合に、このようなマップされた範囲を解放します。これは、ポート\_CONFIGURATION\_INFORMATION **SystemIoBusNumber**値で示されます。

- [**ScsiPortGetUncachedExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetuncachedextension)は、システムとバスマスタ HBA の間で共有される DMA バッファーを割り当てることができます。

これらの4つのルーチンに加えて、ミニポートドライバーの*HwScsiFindAdapter*ルーチンからのみ呼び出すことができるルーチンと、コントロールの種類が**ScsiSetRunningConfig**の場合は*HwScsiAdapterControl* *から呼び出す*ことができるルーチンが1つあります。

- [**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetbusdata)は、バス相対デバイスメモリ (アクセス) 範囲、割り込みベクターまたは IRQL、DMA チャネルまたはポートなどの BUS_DATA_TYPE 固有の構成情報を取得します。

これらの**ScsiPort**_Xxx_ルーチンの詳細については、「 [SCSI ポートドライバーのサポートルーチン](scsi-port-driver-support-routines.md)」を参照してください。

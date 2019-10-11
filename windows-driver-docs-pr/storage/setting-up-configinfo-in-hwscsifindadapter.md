---
title: HwScsiFindAdapter での ConfigInfo の設定
description: HwScsiFindAdapter での ConfigInfo の設定
ms.assetid: f9c5d23d-feab-4cc4-9cd9-29c21d4fdf0b
keywords:
- HwScsiFindAdapter
- SCSI ミニポートドライバー WDK 記憶域、HwScsiFindAdapter
- ConfigInfo
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5d49d172f273074327c5df505cabaea422fd5106
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252450"
---
# <a name="setting-up-configinfo-in-hwscsifindadapter"></a>HwScsiFindAdapter での ConfigInfo の設定

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンは、 [**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)を呼び出して、サポートされている HBA について、POS データや EISA 構成データなど、返されたバスタイプ固有の構成情報を調べることができます。

入力 PORT_CONFIGURATION_INFORMATION ( *Configinfo*バッファー) 内の**accessranges**要素がポートドライバーによって入力されている場合、 *HwScsiFindAdapter*ルーチンはバス相対アクセス範囲をに[**マップする必要があります。ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)は、返された論理アクセス範囲アドレスを使用して HBA と通信します。 アクセス範囲アドレスがポートドライバーによって指定されている場合、 *HwScsiFindAdapter*は、その i/o バス上の他の場所にある hba をスキャンすることはできません。

また、ポートドライバーがアクセス範囲の値を提供する場合、 *HwScsiFindAdapter*では*HwContext*パラメーターを使用できません。 通常、このようなアクセス範囲の値には、プラグアンドプレイ環境を示す追加の構成情報が付随します。 このような環境では、ミニポートドライバーの[**Driverentry**](driverentry-of-scsi-miniport-driver.md)ルーチンが返された後に*HwScsiFindAdapter*が呼び出されているため、 *HwContext*ポインターは無効になります。 ポートドライバーからアクセス範囲の値がゼロで、サポートされている Hba をスキャンするドライバーだけが、 *HwContext*ポインターを安全に使用できます。

入力[PORT_CONFIGURATION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)に、以前に[HW_INITIALIZATION_DATA (SCSI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)のミニポートドライバーによって提供された構成情報が含まれていない場合、 *HwScsiFindAdapter*は、によって返された値を使用できます。[**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)または必要に応じて、HBA がシステムを使用している場合は、 **BusInterruptLevel**または**BusInterruptVector**、 **DmaChannel** 、または**DmaPort**に対して、ミニポートドライバーで定義された既定**値を設定**します。DMA および**InitiatorBusId**。

*HwScsiFindAdapter*は、このようなミニポートドライバーが提供するアクセス範囲を、バス上の HBA にアクセス*する前に*安全に使用できるかどうかを確認するために、 [**ScsiPortValidateRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportvalidaterange)を呼び出す必要があります。 **ScsiPortValidateRange**が**TRUE**を返す場合、ミニポートドライバーは[**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)を呼び出して範囲をマップし、返された論理アドレスを **ScsiPortRead * ** * * xxx および/または **ScsiPortWrite * * * xxx*の呼び出しで使用できます。i/o バス上の HBA がサポートされているかどうかを判断します。 **ScsiPortValidateRange**から**FALSE**が返された場合、ミニポートドライバーは、これらのバス相対アクセス範囲の値をマップして使用することはできません。

同様に、ポートドライバーが非列挙型バス上のデバイスを検出するためにプラグアンドプレイミニポートドライバーを呼び出す場合、 **ScsiPortGetDeviceBase**を呼び出す前に、ミニポートドライバーがアクセス範囲を検証する必要があります。

ポートドライバーが割り込み構成情報を提供する場合、ミニポートドライバーはそれを受け入れる必要があります。また、HBA がプログラミング可能な割り込み構成をサポートしている場合、は、指定された割り込み値を使用するように HBA をプログラミングする必要があります。 割り込み構成が指定されていない場合は、0または値 SP_UNINITIALIZED_VALUE によって示されます。また、HBA がジャンパーを使用した割り込み選択をサポートしている場合、またはゼロ以外の既定値を指定する必要がある場合は、ミニポートドライバーは HBA を照会する必要があります。割り込み構成。ただし、HBA で割り込みが使用されていない場合は除きます。 割り込み構成値0は、ミニポートドライバーがポーリングモードでその HBA を制御していることを示します。

*HwScsiFindAdapter*がサポート可能な hba を検出すると、このルーチンは、PORT_CONFIGURATION_INFORMATION で、hba および指定された**AdapterInterfaceType**に適した関連するメンバーを入力する必要があります。 アクセス範囲を提供するミニポートドライバーは、 **Accessrange情報**を入力する必要があります。各**accessrangeelement**のバス相対**rangestart**値を[**ScsiPortConvertUlongToPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportconvertulongtophysicaladdress)の前に変換します。PORT_CONFIGURATION_INFORMATION の範囲にバス相対ベースアドレスを設定します。

サポートされている HBA の場合、 *HwScsiFindAdapter*は、 **ScsiPortGetDeviceBase**によって返された、マップされた論理範囲のアドレスをミニポートドライバーのデバイス拡張機能に保存する必要があります。 すべてのミニポートドライバーは、これらのマップされたシステムアドレスを使用して HBA と通信するために、**ScsiPortRead ** * * xxx および **ScsiPortWrite * * xxx*を呼び出す必要があります。

I/o スペースで正常に検証され、マップされた範囲ごとに、ミニポートドライバーは **ScsiPortRead/WritePort * * * Xxx*ルーチンを呼び出して、HBA と通信します。 このようなメモリ領域の範囲ごとに、ミニポートドライバーは **ScsiPortRead/WriteRegister * * * Xxx*を呼び出します。

"互換性のある" HBA の場合、 *HwScsiFindAdapter*は入力 atdisk を確認する必要があります。 **メンバーを要求し**、値を**TRUE**にリセットして "AT" 範囲を要求しようとしました。

---
title: SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン
description: SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン
ms.assetid: c89ad751-ff29-4aa7-b907-cb490d060906
keywords:
- HwScsiFindAdapter
- SCSI ミニポートドライバー WDK 記憶域、HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ca3badd855d43ebf226442fcb8d892a6066cce8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842671"
---
# <a name="scsi-miniport-drivers-hwscsifindadapter-routine"></a>SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsifindadapter_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIFINDADAPTER_ROUTINE_KG"></span>


オペレーティングシステム固有のポートドライバーは、ミニポートドライバーのハードウェア\_初期化\_データ (SCSI) によって可能な限り、構成情報バッファー内の[ **\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)を格納します[ **。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)構成情報バッファーへのポインターを使用して指定された*HwScsiFindAdapter*ルーチンを呼び出す前に、システム内の仕様およびその他のソース。

一般に、 *HwScsiFindAdapter*ルーチンは、指定された構成情報を使用するか、**ScsiPort * * Xxx*を呼び出すために十分な構成情報を収集して i/o 上の HBA をサポートするかどうかを判断する役割を担います。ポート\_構成の**SystemIoBusNumber**によって識別されるバスは、ポートドライバーによって提供される情報\_ます。 その場合、 *HwScsiFindAdapter*は、ポート\_構成\_情報でサポートされている HBA の残りの構成情報を入力する役割を担います。ドライバーは、その HBA についての状態を確認し、制御を返す前に *、パラメーターを*適切な値に設定します。

詳細については、「 [**PORT\_CONFIGURATION\_information**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information) and [*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 」を参照してください。

 

 





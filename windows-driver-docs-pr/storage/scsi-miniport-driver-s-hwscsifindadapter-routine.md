---
title: SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン
description: SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン
ms.assetid: c89ad751-ff29-4aa7-b907-cb490d060906
keywords:
- HwScsiFindAdapter
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe8a1217bab4dfc0eb5362a974b3d7272bdc0e1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385225"
---
# <a name="scsi-miniport-drivers-hwscsifindadapter-routine"></a>SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsifindadapter_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIFINDADAPTER_ROUTINE_KG"></span>


オペレーティング システム固有のポートのドライバーをできるだけ多くの設定、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)ほど構成情報バッファーからことができます、ミニポート ドライバーの[ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)仕様とその他のソースを呼び出す前に、システムで、指定された*HwScsiFindAdapter*構成情報バッファーへのポインターとルーチン。

一般に、 *HwScsiFindAdapter*ルーチンは、指定された構成情報を使用するためや呼び出し元の責任 **ScsiPort * * * Xxx*に必要な構成情報を収集するには識別される I/O バスで HBA がサポートするかどうかを確認、 **SystemIoBusNumber**ポート\_構成\_ポート ドライバーによって提供される情報。 そうである場合*HwScsiFindAdapter*ポートでサポートされている HBA の残りの構成情報の入力を担当\_構成\_については、ミニポート ドライバーのセットアップデバイス ドライバーが決定した状態の設定およびその HBA に関する拡張機能、*再度*に制御を返す前に適切な値のパラメーター。

参照してください[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)と[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))詳細についてはします。

 

 





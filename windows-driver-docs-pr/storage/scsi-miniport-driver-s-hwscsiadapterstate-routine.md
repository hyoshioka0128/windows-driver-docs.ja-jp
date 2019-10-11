---
title: SCSI ミニポート ドライバーの HwScsiAdapterState ルーチン
description: SCSI ミニポート ドライバーの HwScsiAdapterState ルーチン
ms.assetid: 359c41ba-b8d9-4e2d-87d7-025db377606b
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiAdapterState
- HwScsiAdapterState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24144f42be36e851d16fb1d348e1cf8ad137c754
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252457"
---
# <a name="scsi-miniport-drivers-hwscsiadapterstate-routine"></a>SCSI ミニポート ドライバーの HwScsiAdapterState ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiadapterstate_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERSTATE_ROUTINE_KG"></span>


NT ベースのオペレーティングシステムでは、[**ハードウェア @ no__t-3INITIALIZATION @ no__t-4DATA (scsi)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)で、このエントリポイントを**NULL**に設定する必要があります ( [scsi ミニポートドライバールーチン](scsi-miniport-driver-routines.md)を参照してください)。次の条件のいずれかが満たされている場合のみです。

-   ミニポートドライバーは、一般にハイエンドの RISC ベースのプラットフォームでのみ検出される i/o バス上で、HBA を接続します。 つまり、x86 専用の Microsoft Windows システムを実行している x86 ベースのプラットフォームには、HBA をサポートする種類の i/o バスがありません。

-   ミニポートドライバーは、x86 専用の Windows システムを実行している x86 ベースのプラットフォームで検出された HBA を駆動しますが、HBA には BIOS も x86 専用のリアルモードドライバーもありません。

それ以外の場合、ミニポートドライバーは、NT ベースのオペレーティングシステムと x86 専用の Microsoft Windows システムの間で移植可能な*HwScsiAdapterState*ルーチンを備えている必要があります。

[**HwScsiAdapterState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85))ルーチンは、x86 システムと保護されたプロセッサモード間の移行時に、x86 専用システムによって要求された HBA の状態を保存および復元する役割を担います。

詳細については、「 [**HwScsiAdapterState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85)) 」を参照してください。

 

 





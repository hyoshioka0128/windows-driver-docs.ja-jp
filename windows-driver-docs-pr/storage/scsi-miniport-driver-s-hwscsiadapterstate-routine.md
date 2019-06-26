---
title: SCSI ミニポート ドライバーの HwScsiAdapterState ルーチン
description: SCSI ミニポート ドライバーの HwScsiAdapterState ルーチン
ms.assetid: 359c41ba-b8d9-4e2d-87d7-025db377606b
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiAdapterState
- HwScsiAdapterState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c3ba2c008086bc2b57de459a7de2f634b334386
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384326"
---
# <a name="scsi-miniport-drivers-hwscsiadapterstate-routine"></a>SCSI ミニポート ドライバーの HwScsiAdapterState ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiadapterstate_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERSTATE_ROUTINE_KG"></span>


NT ベースのオペレーティング システムのミニポート ドライバーにこのエントリ ポイントを設定する必要があります**NULL**で、 [ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data) (参照してください[必須およびオプションの SCSI ミニポート ドライバー ルーチン](required-and-optional-scsi-miniport-driver-routines.md))、次の条件のいずれかを保持している場合のみ。

-   ミニポート ドライバーには、ハイエンドの RISC ベースのプラットフォームのみによく見られる、I/O バスに接続する HBA がドライブします。 つまり、x86 専用の Microsoft Windows システムを実行している x86 ベースのプラットフォームには、HBA をサポートする型の I/O バスの必要はありません。

-   ミニポート ドライバー ドライブ HBA を x86 専用の Windows システムを実行している x86 ベースのプラットフォームでは見つかりませんでしたが、HBA、x86 専用のリアル モード ドライバーと BIOS のどちらでもないです。

それ以外の場合、ミニポート ドライバーが必要、 *HwScsiAdapterState* NT ベースのオペレーティング システムおよび x86 専用の Microsoft Windows システムの間で移植できるルーチン。

A [ **HwScsiAdapterState** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85))ルーチンは、x86 との間の遷移中に、x86 専用のシステムからの要求での保存と、その HBA の状態を復元する責任を負います実数部と保護されているプロセッサ モード。

参照してください[ **HwScsiAdapterState** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85))詳細についてはします。

 

 





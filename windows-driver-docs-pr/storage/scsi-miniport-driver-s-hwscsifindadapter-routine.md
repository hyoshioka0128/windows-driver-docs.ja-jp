---
title: SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン
description: SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン
ms.assetid: c89ad751-ff29-4aa7-b907-cb490d060906
keywords:
- HwScsiFindAdapter
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3dea9567022abb481e6dbcacc6b9774ce24e469
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527223"
---
# <a name="scsi-miniport-drivers-hwscsifindadapter-routine"></a>SCSI ミニポート ドライバーの HwScsiFindAdapter ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsifindadapter_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIFINDADAPTER_ROUTINE_KG"></span>


オペレーティング システム固有のポートのドライバーをできるだけ多くの設定、 [**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563900)ほど構成情報バッファーからことができます、ミニポート ドライバーの[ **HW\_初期化\_データ (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456)仕様とその他のソースを呼び出す前に、システムで、指定された*HwScsiFindAdapter*構成情報バッファーへのポインターとルーチン。

一般に、 *HwScsiFindAdapter*ルーチンは、指定された構成情報を使用するためや呼び出し元の責任 **ScsiPort * * * Xxx*に必要な構成情報を収集するには識別される I/O バスで HBA がサポートするかどうかを確認、 **SystemIoBusNumber**ポート\_構成\_ポート ドライバーによって提供される情報。 そうである場合*HwScsiFindAdapter*ポートでサポートされている HBA の残りの構成情報の入力を担当\_構成\_については、ミニポート ドライバーのセットアップデバイス ドライバーが決定した状態の設定およびその HBA に関する拡張機能、*再度*に制御を返す前に適切な値のパラメーター。

参照してください[**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563900)と[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)詳細についてはします。

 

 





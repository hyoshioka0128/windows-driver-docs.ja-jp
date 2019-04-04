---
title: ストレージのフィルター ドライバーの PnP 開始の処理
description: ストレージのフィルター ドライバーの PnP 開始の処理
ms.assetid: 02a87fec-772d-4416-bd3a-5c7f98e8d55e
keywords:
- 記憶域フィルター ドライバー WDK、PnP
- フィルター ドライバー WDK の記憶域、PnP
- SFD WDK の記憶域、PnP
- PnP WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57aa07a455768c97524442764a0f1cb016a33cb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558417"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>ストレージのフィルター ドライバーの PnP 開始の処理


## <span id="ddk_handling_pnp_start_in_a_storage_filter_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_FILTER_DRIVER_KG"></span>


記憶域フィルター ドライバー (SFD) がデバイスに固有の初期化を実行し、PnP マネージャーを呼び出すときにそのデバイスの拡張機能を設定、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)開始要求をルーチン ([ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)で[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749))。 SFD は、ストレージ クラス ドライバーのように開始要求と同じ方法を処理します。

ストレージ クラス ドライバーの開始要求を処理してそのデバイスの拡張機能を設定する方法については、[ストレージ クラス ドライバー](storage-class-drivers.md)を参照してください。 PnP 開始要求の処理の詳細については、[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)を参照してください。

 

 





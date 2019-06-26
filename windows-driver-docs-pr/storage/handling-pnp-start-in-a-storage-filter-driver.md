---
title: 記憶域フィルター ドライバーでの PnP 開始の処理
description: 記憶域フィルター ドライバーでの PnP 開始の処理
ms.assetid: 02a87fec-772d-4416-bd3a-5c7f98e8d55e
keywords:
- 記憶域フィルター ドライバー WDK、PnP
- フィルター ドライバー WDK の記憶域、PnP
- SFD WDK の記憶域、PnP
- PnP WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09933762e0eae8138ac1d9a894081e33fe459469
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378494"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>記憶域フィルター ドライバーでの PnP 開始の処理


## <span id="ddk_handling_pnp_start_in_a_storage_filter_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_FILTER_DRIVER_KG"></span>


記憶域フィルター ドライバー (SFD) がデバイスに固有の初期化を実行し、PnP マネージャーを呼び出すときにそのデバイスの拡張機能を設定、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)開始要求をルーチン ([ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)で[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 SFD は、ストレージ クラス ドライバーのように開始要求と同じ方法を処理します。

ストレージ クラス ドライバーの開始要求を処理してそのデバイスの拡張機能を設定する方法については、次を参照してください。[ストレージ クラス ドライバー](storage-class-drivers.md)します。 PnP 開始要求の処理の詳細については、次を参照してください。[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)します。

 

 





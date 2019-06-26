---
title: 記憶域フィルター ドライバーの DriverEntry ルーチン
description: 記憶域フィルター ドライバーの DriverEntry ルーチン
ms.assetid: 801daf42-259d-45ab-a5c5-88acb2d35bef
keywords:
- 記憶域フィルター ドライバー WDK、DriverEntry
- フィルター ドライバー WDK ストレージ、DriverEntry
- DriverEntry SFD WDK ストレージ
- DriverEntry WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 524b38474d6790acff446706465183a43e0353e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376688"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>記憶域フィルター ドライバーの DriverEntry ルーチン


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


などの他のカーネル モード ドライバー、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ストレージ フィルター ドライバー (SFD) のルーチンは入力のドライバ オブジェクトでのディスパッチと他のエントリ ポイントを定義する必要があります。 必要に応じて、SFD を割り当てることがドライバー適切なサイズのオブジェクトの拡張機能を呼び出して[ **IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatedriverobjectextension)ドライバーの拡張機能を後で使用するために、入力のレジストリ パスをコピーし、存在する場合は、他のドライバーにより決定されたデータを使用してドライバー拡張機能を初期化します。

PnP ドライバーの詳細については[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンを参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)します。

 

 





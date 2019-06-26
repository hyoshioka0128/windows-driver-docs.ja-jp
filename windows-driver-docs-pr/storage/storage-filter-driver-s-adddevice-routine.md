---
title: 記憶域フィルター ドライバーの AddDevice ルーチン
description: 記憶域フィルター ドライバーの AddDevice ルーチン
ms.assetid: 7970fb3e-4e4c-4ff7-9738-e09454a864c4
keywords:
- 記憶域フィルター ドライバー WDK、AddDevice
- フィルター ドライバー WDK ストレージ、AddDevice
- AddDevice SFD WDK ストレージ
- AddDevice ルーチン WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 244e6799c4177f13a121257becbc2908ca1e506a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368205"
---
# <a name="storage-filter-drivers-adddevice-routine"></a>記憶域フィルター ドライバーの AddDevice ルーチン


## <span id="ddk_storage_filter_driver_s_adddevice_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_ADDDEVICE_ROUTINE_KG"></span>


PnP マネージャー呼び出し、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ドライバーによって制御されるデバイスを検出した場合に、記憶域フィルター ドライバーの日常的な。 *AddDevice*ストレージ フィルター ドライバー (SFD) のルーチンは、記憶域クラス ドライバーに似ていますが、デバイスを要求する必要がありますしない点が異なります (SRB\_関数\_要求\_デバイス)。

記憶域クラス ドライバーのについて[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンを参照してください[ストレージ クラス ドライバー](storage-class-drivers.md)します。 PnP ドライバーの詳細について*AddDevice*ルーチンを参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)します。

 

 





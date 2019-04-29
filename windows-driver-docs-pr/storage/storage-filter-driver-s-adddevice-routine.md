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
ms.openlocfilehash: 2b257863243c07fc5d2233f7c30973e7dac01ace
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331715"
---
# <a name="storage-filter-drivers-adddevice-routine"></a>記憶域フィルター ドライバーの AddDevice ルーチン


## <span id="ddk_storage_filter_driver_s_adddevice_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_ADDDEVICE_ROUTINE_KG"></span>


PnP マネージャー呼び出し、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ドライバーによって制御されるデバイスを検出した場合に、記憶域フィルター ドライバーの日常的な。 *AddDevice*ストレージ フィルター ドライバー (SFD) のルーチンは、記憶域クラス ドライバーに似ていますが、デバイスを要求する必要がありますしない点が異なります (SRB\_関数\_要求\_デバイス)。

記憶域クラス ドライバーのについて[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンを参照してください[ストレージ クラス ドライバー](storage-class-drivers.md)します。 PnP ドライバーの詳細について*AddDevice*ルーチンを参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)します。

 

 





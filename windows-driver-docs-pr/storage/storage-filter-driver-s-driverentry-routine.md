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
ms.openlocfilehash: 5ae09667dc7bd14b99fc8628900d2a8211f5d7dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384831"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>記憶域フィルター ドライバーの DriverEntry ルーチン


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


などの他のカーネル モード ドライバー、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ストレージ フィルター ドライバー (SFD) のルーチンは入力のドライバ オブジェクトでのディスパッチと他のエントリ ポイントを定義する必要があります。 必要に応じて、SFD を割り当てることがドライバー適切なサイズのオブジェクトの拡張機能を呼び出して[ **IoAllocateDriverObjectExtension**](https://msdn.microsoft.com/library/windows/hardware/ff548233)ドライバーの拡張機能を後で使用するために、入力のレジストリ パスをコピーし、存在する場合は、他のドライバーにより決定されたデータを使用してドライバー拡張機能を初期化します。

PnP ドライバーの詳細については[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンを参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)します。

 

 





---
title: 記憶域周辺機器への PnP 要求の処理
description: 記憶域周辺機器への PnP 要求の処理
ms.assetid: 9c7ea576-11e6-46d7-b04c-ce412a0fc569
keywords:
- 記憶域 WDK 周辺機器、PnP 要求
- 記憶域周辺機器 WDK、PnP 要求
- PnP WDK ストレージ
- プラグ アンド プレイ WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f111fc01d7d9c7d0fc0e28caf05f1c3512bcaacc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390900"
---
# <a name="handling-pnp-requests-to-storage-peripherals"></a>記憶域周辺機器への PnP 要求の処理


## <span id="ddk_handling_pnp_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_PNP_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


記憶域クラス ドライバーの*DispatchPnP* PnP 要求への応答では、次のルーチンが担当します。

-   開始要求に対する応答でそのデバイスを起動 (IRP\_MJ\_PNP IRP の\_MN\_開始\_デバイス)。 参照してください[処理、ストレージ クラス ドライバーの PnP 開始](handling-pnp-start-in-a-storage-class-driver.md)します。

-   削除要求への応答でそのデバイスを削除する (IRP\_MJ\_PNP IRP の\_MN\_削除\_デバイス)。 参照してください[ストレージ クラス ドライバーの RemoveDevice ルーチン](storage-class-driver-s-removedevice-routine.md)します。

-   そのデバイスは、システムのページング ファイルを含めることができます場合、ページングのポケットベルによる通知の要求に対する応答で、デバイスの拡張機能内のパスの通知回数をカウントする (IRP\_MJ\_で PNP [ **IRP\_。MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)) と、次の下位ドライバーへの要求を転送します。

-   クエリの削除、クエリ停止要求を処理し、システムのページング ファイルや休止状態ファイルが、デバイスが含まれる場合は、このような要求を失敗します。 ドライバーも失敗するクエリの削除要求のクラッシュ ダンプ、そのデバイスが要求した場合クラッシュ ダンプを無効にこのようなデバイスを削除するため。

記憶域クラス ドライバーは、クエリの PnP、cancel、および次の下位のドライバーを (クエリが失敗した要求) を除く停止要求を転送します。

 

 





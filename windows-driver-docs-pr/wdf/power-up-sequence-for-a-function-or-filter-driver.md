---
title: 機能ドライバーまたはフィルター ドライバーの電源投入シーケンス
description: 機能ドライバーまたはフィルター ドライバーの電源投入シーケンス
ms.assetid: 3E904641-A1E2-400C-A201-2D1D2D359657
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee3e01022ba97e1c3778204f41b5a34ddb68186d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376340"
---
# <a name="power-up-sequence-for-a-function-or-filter-driver"></a>機能ドライバーまたはフィルター ドライバーの電源投入シーケンス


次の図は、図の下部にあるデバイスが挿入された状態から開始、完全に operational 状態へのデバイスの追加時に、フレームワーク、KMDF 関数またはフィルター ドライバーのイベントのコールバック関数を呼び出す順序を示します。

![関数またはフィルター ドライバーのデバイスの列挙と電源投入シーケンス](images/fdo-fido-powerup.png)

広範な水平の線は、デバイスの起動に関連するステップをマークします。 図の左側にある列について、手順を説明し、右側の列には、そのイベントのコールバックが一覧表示されます。

図の下部には、デバイスは、システムに存在しません。 フレームワークを呼び出してドライバーの開始、ユーザーがデバイスを挿入するとき[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック、ドライバーは、デバイスを表すデバイス オブジェクトを作成できるようにします。 フレームワークでは、ドライバーのコールバック ルーチンを呼び出すことによって、デバイスは稼働までのシーケンスを経由の進行が続行されます。 フレームワークは、ために下から順に順番の図に示すようにイベント コールバックを呼び出すことに注意してください[ *EvtDeviceFilterRemoveResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)前に呼び出されます[ *。EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)という具合です。 デバイスがリソースを再調整を停止したか、物理的に存在していた場合は、低電力状態にすべての手順は、図に示すように、必要です。

 

 






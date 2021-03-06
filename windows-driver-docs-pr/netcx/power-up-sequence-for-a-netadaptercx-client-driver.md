---
title: NetAdapterCx クライアント ドライバーの電源投入シーケンス
description: NetAdapterCx クライアント ドライバーの電源投入シーケンス
ms.assetid: 86694F6B-9AE4-4FDB-A4BB-9B7ACBC0B1DA
keywords:
- 電源投入シーケンス NetAdapterCx クライアント ドライバー、NetAdapterCx クライアント ドライバーの電源投入シーケンス、NetCx クライアント ドライバーの電源投入シーケンス
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7130e35986eaa915f91a7c85ddfa17e1e2895ff0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382817"
---
# <a name="power-up-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーの電源投入シーケンス

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の図を NetAdapterCx 関数を呼び出すクライアント ドライバーのイベント コールバックにときにデバイスを完全に動作の状態の図の下部にあるデバイスが到着した状態から開始順序を示します。

<img src="images/netadaptercx-powerup.png" alt="Device enumeration and power-up sequence for NetAdapterCx client driver" title="NetAdapterCx クライアント ドライバーのデバイスの列挙と電源投入シーケンス" style="width: 600px;"/>

広範な水平の線は、デバイスの起動に関連するステップをマークします。 図の左側にある列について、手順を説明し、右側の列には、そのイベントのコールバックが一覧表示されます。 青色のテキストでマークされている手順は、他の手順はすべて WDF ベースのドライバーに共通 NetAdapterCx に固有です。

図の下部には、デバイスは、システムに存在しません。 フレームワークを呼び出してドライバーの開始、ユーザーがデバイスを挿入するとき[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック、ドライバーは、デバイスを表すデバイス オブジェクトを作成できるようにします。 フレームワークでは、ドライバーのコールバック ルーチンを呼び出すことによって、デバイスは稼働までのシーケンスを経由の進行が続行されます。 フレームワークは、ために下から順に順番の図に示すようにイベント コールバックを呼び出すことに注意してください[ *EvtDeviceFilterRemoveResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)前に呼び出されます[ *。EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)という具合です。 デバイスがリソースを再調整を停止したか、物理的に存在していた場合は、低電力状態にすべての手順は、図に示すように、必要です。


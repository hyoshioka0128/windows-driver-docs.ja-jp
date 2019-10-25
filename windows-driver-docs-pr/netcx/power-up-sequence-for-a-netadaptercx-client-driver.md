---
title: NetAdapterCx クライアント ドライバーの電源投入シーケンス
description: NetAdapterCx クライアント ドライバーの電源投入シーケンス
ms.assetid: 86694F6B-9AE4-4FDB-A4BB-9B7ACBC0B1DA
keywords:
- NetAdapterCx クライアントドライバーの電源シーケンス, NetAdapterCx クライアントドライバーの電源シーケンス, NetCx クライアントドライバー用の電源設定のシーケンスです。
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: bac2adbf13381a25cb229709dbe5271e11ac9d10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835465"
---
# <a name="power-up-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーの電源投入シーケンス

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の図は、デバイスを完全に動作状態にするときに、図の下部にあるデバイスが到着した状態から開始するときに、NetAdapterCx がクライアントドライバーのイベントコールバック関数を呼び出す順序を示しています。

<img src="images/netadaptercx-powerup.png" alt="Device enumeration and power-up sequence for NetAdapterCx client driver" title="NetAdapterCx クライアントドライバーのデバイス列挙と電源シーケンス" style="width: 600px;"/>

水平線は、デバイスの起動に関係する手順を示しています。 図の左側の列には手順が記述されており、右側の列には、それを実現するイベントコールバックが一覧表示されます。 青いテキストでマークされた手順は NetAdapterCx に固有であり、他の手順はすべての WDF ベースのドライバーに共通です。

図の下部には、デバイスがシステム上に存在していません。 ユーザーがデバイスを挿入すると、まず、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックを呼び出して、ドライバーがデバイスを表すデバイスオブジェクトを作成できるようにします。 フレームワークは、デバイスが動作するまで順番を進めることで、ドライバーのコールバックルーチンの呼び出しを続けます。 フレームワークは、図に示すように、下から順にイベントコールバックを呼び出します。したがって、 [*EvtDeviceFilterRemoveResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)は[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)の前に呼び出されます。 デバイスがリソースの再調整のために停止された場合、または物理的に存在するが低電力状態の場合は、図に示すように、すべての手順が必要になるわけではありません。


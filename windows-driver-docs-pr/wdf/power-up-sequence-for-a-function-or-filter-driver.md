---
title: 機能ドライバーまたはフィルター ドライバーの電源投入シーケンス
description: 機能ドライバーまたはフィルター ドライバーの電源投入シーケンス
ms.assetid: 3E904641-A1E2-400C-A201-2D1D2D359657
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b966bdc1091be2d9393cb5798a6bdf74c59f7e8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842238"
---
# <a name="power-up-sequence-for-a-function-or-filter-driver"></a>機能ドライバーまたはフィルター ドライバーの電源投入シーケンス


次の図は、デバイスを完全に動作状態にするときに、図の下部にあるデバイスが挿入された状態から開始するときに、フレームワークが WDF (KMDF and UMDF V2) 関数またはフィルタードライバーのイベントコールバック関数を呼び出す順序を示しています。

![関数またはフィルタードライバーのデバイス列挙と電源投入シーケンス](images/fdo-fido-powerup.png)

水平線は、デバイスの起動に関係する手順を示しています。 図の左側の列には手順が記述されており、右側の列には、それを実現するイベントコールバックが一覧表示されます。

図の下部には、デバイスがシステム上に存在していません。 ユーザーがデバイスを挿入すると、まず、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックを呼び出して、ドライバーがデバイスを表すデバイスオブジェクトを作成できるようにします。 フレームワークは、デバイスが動作するまで順番を進めることで、ドライバーのコールバックルーチンの呼び出しを続けます。 フレームワークは、図に示すように、下から順にイベントコールバックを呼び出します。したがって、 [*EvtDeviceFilterRemoveResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)は[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)の前に呼び出されます。 デバイスがリソースの再調整のために停止された場合、または物理的に存在するが低電力状態の場合は、図に示すように、すべての手順が必要になるわけではありません。

 

 






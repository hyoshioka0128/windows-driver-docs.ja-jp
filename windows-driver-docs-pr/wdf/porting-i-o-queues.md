---
title: I/O キューの移植
description: I/O キューの移植
ms.assetid: 90319342-5FAB-451B-BCA1-B273B81418DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01923c4f80e55c3adbeb07ac40c0dd0cf7e5c8cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842255"
---
# <a name="porting-io-queues"></a>I/O キューの移植


WDF ドライバーは、キューを作成し、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックに i/o イベントコールバックを登録します。 既定では、各 i/o queue オブジェクトはデバイスオブジェクトの子です。 WDF ドライバーでは、キューごとに次のタスクを構成できます。

-   キューに送信される i/o 要求の種類。
-   要求が並列で (到着するとすぐに)、順番に (一度に1つずつ)、または手動で (ドライバー要求時に) 手動でディスパッチされるかどうか。
-   I/o イベントのコールバックルーチンが同時に呼び出されるか、直列で呼び出されるか。
-   フレームワークまたはドライバーが、システムとデバイスの電源切り替えによってキューを管理するかどうか。

キューの作成の詳細については、「 [I/o キューの作成](creating-i-o-queues.md)」を参照してください。

 

 






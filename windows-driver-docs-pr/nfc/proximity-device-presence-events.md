---
title: 近接通信デバイスのプレゼンス イベント
description: 近接通信デバイスのプレゼンス イベント
ms.assetid: 8E0E44D5-E6DD-4385-988E-EFDAA75C6D59
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f86f1908453b4019c46ec0716aa950afb03693b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386516"
---
# <a name="proximity-device-presence-events"></a>近接通信デバイスのプレゼンス イベント


NFP プロバイダーは、到達または近接デバイス (トリガーの動作のウィンドウ) の出発地、NFP プロバイダーが検出されたときに、イベントを受信するクライアントを有効にします。 NFP プロバイダーは、近接性を検出するたびに、プロバイダーが 1 つまたは複数の近接デバイスと現在通信できることを意味するプロバイダー発行する必要を*DeviceArrived*イベント。 NFP プロバイダーは、近接デバイスと通信できません、発行が必要な*DeviceDeparted*イベント。

NFP プロバイダーも、公開されたメッセージはだけを転送した 1 回、デバイスが近接内では正しく確保するために、近接デバイスの存在を追跡する必要があります。 これらのイベントは、同じメトリックに基づく必要があります。 同時に複数の近接デバイスと通信できるように、NFP プロバイダー、プレゼンスのイベントはすべてプレゼンスの集計を設定してください。 プロバイダーは、0 ~ N 同時に近接デバイスをサポートする場合、イベントは 0-1 と 1 対 0 現在近接デバイスからの移行にのみ配信されます。 NFC はサポートされていないことこれに注意してください。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  


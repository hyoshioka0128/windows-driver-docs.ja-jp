---
title: 近接デバイス プレゼンス イベント
description: 近接デバイス プレゼンス イベント
ms.assetid: 8E0E44D5-E6DD-4385-988E-EFDAA75C6D59
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 110f68cbc4d0a7d590415d3943310131b1a4fdfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528493"
---
# <a name="proximity-device-presence-events"></a>近接デバイス プレゼンス イベント


NFP プロバイダーは、到達または近接デバイス (トリガーの動作のウィンドウ) の出発地、NFP プロバイダーが検出されたときに、イベントを受信するクライアントを有効にします。 NFP プロバイダーは、近接性を検出するたびに、プロバイダーが 1 つまたは複数の近接デバイスと現在通信できることを意味するプロバイダー発行する必要を*DeviceArrived*イベント。 NFP プロバイダーは、近接デバイスと通信できません、発行が必要な*DeviceDeparted*イベント。

NFP プロバイダーも、公開されたメッセージはだけを転送した 1 回、デバイスが近接内では正しく確保するために、近接デバイスの存在を追跡する必要があります。 これらのイベントは、同じメトリックに基づく必要があります。 同時に複数の近接デバイスと通信できるように、NFP プロバイダー、プレゼンスのイベントはすべてプレゼンスの集計を設定してください。 プロバイダーは、0 ~ N 同時に近接デバイスをサポートする場合、イベントは 0-1 と 1 対 0 現在近接デバイスからの移行にのみ配信されます。 NFC はサポートされていないことこれに注意してください。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  


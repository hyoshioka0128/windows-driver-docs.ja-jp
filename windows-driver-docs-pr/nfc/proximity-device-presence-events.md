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
ms.openlocfilehash: d0b7cd6349b78c244156c4851e9d741712854b67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834535"
---
# <a name="proximity-device-presence-events"></a>近接通信デバイスのプレゼンス イベント


NFP プロバイダーは、NFP プロバイダーが近接デバイスの到着または出発点 (トリガーを起動するアクションのウィンドウ) を検出するたびにイベントを受信できるようにします。 NFP プロバイダーが近接を検出するたびに、プロバイダーが現在1つ以上の近接デバイスと通信できることを意味します。プロバイダーは*DeviceArrived*イベントを発行する必要があります。 NFP プロバイダーが近接デバイスと通信できなくなった場合は、 *devicedeparted*イベントを発行する必要があります。

また、送信されたメッセージが近接している間に1回だけ転送されるようにするために、近接デバイスの存在を追跡する必要もあります。 これらのイベントは、同じメトリックに基づいている必要があります。 複数の近接デバイスと同時に通信できるようになった NFP プロバイダーの場合、プレゼンスイベントはすべての存在の集約である必要があります。 プロバイダーが同時にデバイスの近接を0から N までサポートしている場合、イベントは、現在近接されているデバイスが 0 ~ 1 で、1 ~ 0 の場合にのみ配信されます。 NFC はこれをサポートしていないことに注意してください。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  


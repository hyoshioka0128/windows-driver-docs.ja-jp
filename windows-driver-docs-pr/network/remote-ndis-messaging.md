---
title: リモート NDIS メッセージング
description: リモート NDIS メッセージング
ms.assetid: 6364a9a1-c65f-463d-971b-cf94cd2a5cde
keywords:
- リモートの NDIS WDK ネットワーク、メッセージング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e95adc44b4e0971fc13ab582fd6c5e94daec086
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385838"
---
# <a name="remote-ndis-messaging"></a>リモート NDIS メッセージング





リモートの NDIS メッセージの 2 種類があります:*制御メッセージ*と*データ メッセージ*します。 コントロール メッセージでは、ホストとリモート NDIS デバイスは、通信チャネル経由で互いと通信を許可します。 データ メッセージでは、ホストとデバイス間の通信に必要なメッセージ データの情報を含むし、データ チャネル経由で伝達されます。

-   **リモートの NDIS コントロール メッセージ**

    NDIS リモート デバイスをホストおよびホストするリモート NDIS デバイス、リモートの NDIS コントロール メッセージを送信できます。 イーサネット 802.3 コネクションレスのデバイスでは、次のリモートの NDIS コントロール メッセージをサポートする必要があります。

    [リモート\_NDIS\_初期化\_メッセージ](https://docs.microsoft.com/previous-versions/ff570624(v=vs.85))

    [リモート\_NDIS\_初期化\_CMPLT](https://docs.microsoft.com/previous-versions/ff570621(v=vs.85))

    [REMOTE\_NDIS\_HALT\_MSG](https://docs.microsoft.com/previous-versions/ff570613(v=vs.85))

    [リモート\_NDIS\_クエリ\_メッセージ](https://docs.microsoft.com/previous-versions/ff570641(v=vs.85))

    [リモート\_NDIS\_クエリ\_CMPLT](https://docs.microsoft.com/previous-versions/ff570638(v=vs.85))

    [REMOTE\_NDIS\_SET\_MSG](https://docs.microsoft.com/previous-versions/ff570654(v=vs.85))

    [リモート\_NDIS\_設定\_CMPLT](https://docs.microsoft.com/previous-versions/ff570651(v=vs.85))

    [REMOTE\_NDIS\_RESET\_MSG](https://docs.microsoft.com/previous-versions/ff570648(v=vs.85))

    [リモート\_NDIS\_リセット\_CMPLT](https://docs.microsoft.com/previous-versions/ff570645(v=vs.85))

    [リモート\_NDIS\_を示す\_状態\_メッセージ](https://docs.microsoft.com/previous-versions/ff570617(v=vs.85))

    [リモート\_NDIS\_KEEPALIVE\_メッセージ](https://docs.microsoft.com/previous-versions/ff570629(v=vs.85))

    [リモート\_NDIS\_KEEPALIVE\_CMPLT](https://docs.microsoft.com/previous-versions/ff570626(v=vs.85))

-   **リモートの NDIS データ メッセージ**

    リモートの NDIS デバイスに含まれているリモートの NDIS データ パケットを使用してデータを送受信する必要があります、[リモート\_NDIS\_パケット\_MSG](https://docs.microsoft.com/previous-versions/ff570635(v=vs.85))メッセージの構造体。 帯域外データだけでなく、ネットワーク経由で移動するデータは、リモートの NDIS データ パケットは含めることもできます。

    (たとえば、802.3) はコネクションレスの両方と、デバイスの接続指向の (たとえば、ATM など) を使用して、同じ**リモート\_NDIS\_パケット\_MSG**容易共通するためにメッセージの構造パケットの処理のコードです。

 

 






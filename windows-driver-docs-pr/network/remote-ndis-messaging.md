---
title: リモート NDIS メッセージング
description: リモート NDIS メッセージング
ms.assetid: 6364a9a1-c65f-463d-971b-cf94cd2a5cde
keywords:
- リモートの NDIS WDK ネットワーク、メッセージング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1c06267e3edc5937ae3161c2683ad1a10f41dd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350836"
---
# <a name="remote-ndis-messaging"></a>リモート NDIS メッセージング





リモートの NDIS メッセージの 2 種類があります:*制御メッセージ*と*データ メッセージ*します。 コントロール メッセージでは、ホストとリモート NDIS デバイスは、通信チャネル経由で互いと通信を許可します。 データ メッセージでは、ホストとデバイス間の通信に必要なメッセージ データの情報を含むし、データ チャネル経由で伝達されます。

-   **リモートの NDIS コントロール メッセージ**

    NDIS リモート デバイスをホストおよびホストするリモート NDIS デバイス、リモートの NDIS コントロール メッセージを送信できます。 イーサネット 802.3 コネクションレスのデバイスでは、次のリモートの NDIS コントロール メッセージをサポートする必要があります。

    [リモート\_NDIS\_初期化\_メッセージ](https://msdn.microsoft.com/library/windows/hardware/ff570624)

    [リモート\_NDIS\_初期化\_CMPLT](https://msdn.microsoft.com/library/windows/hardware/ff570621)

    [REMOTE\_NDIS\_HALT\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570613)

    [リモート\_NDIS\_クエリ\_メッセージ](https://msdn.microsoft.com/library/windows/hardware/ff570641)

    [リモート\_NDIS\_クエリ\_CMPLT](https://msdn.microsoft.com/library/windows/hardware/ff570638)

    [REMOTE\_NDIS\_SET\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570654)

    [リモート\_NDIS\_設定\_CMPLT](https://msdn.microsoft.com/library/windows/hardware/ff570651)

    [REMOTE\_NDIS\_RESET\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570648)

    [リモート\_NDIS\_リセット\_CMPLT](https://msdn.microsoft.com/library/windows/hardware/ff570645)

    [リモート\_NDIS\_を示す\_状態\_メッセージ](https://msdn.microsoft.com/library/windows/hardware/ff570617)

    [リモート\_NDIS\_KEEPALIVE\_メッセージ](https://msdn.microsoft.com/library/windows/hardware/ff570629)

    [リモート\_NDIS\_KEEPALIVE\_CMPLT](https://msdn.microsoft.com/library/windows/hardware/ff570626)

-   **リモートの NDIS データ メッセージ**

    リモートの NDIS デバイスに含まれているリモートの NDIS データ パケットを使用してデータを送受信する必要があります、[リモート\_NDIS\_パケット\_MSG](https://msdn.microsoft.com/library/windows/hardware/ff570635)メッセージの構造体。 帯域外データだけでなく、ネットワーク経由で移動するデータは、リモートの NDIS データ パケットは含めることもできます。

    (たとえば、802.3) はコネクションレスの両方と、デバイスの接続指向の (たとえば、ATM など) を使用して、同じ**リモート\_NDIS\_パケット\_MSG**容易共通するためにメッセージの構造パケットの処理のコードです。

 

 






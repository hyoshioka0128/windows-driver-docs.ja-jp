---
title: RDMA でのバック グラウンド読み取り
description: RDMA は、CPU 使用率を最小限に抑える高スループットで低待機時間の通信を実現するネットワークテクノロジです。
ms.assetid: 583A806D-B7E8-40F5-9CEB-406FAEE8B6C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efdec7929e1af40f2918c750a72ab22b137ce373
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210862"
---
# <a name="background-reading-on-rdma"></a>RDMA でのバック グラウンド読み取り


RDMA は、CPU 使用率を最小限に抑える高スループットで低待機時間の通信を実現するネットワークテクノロジです。 NDK で現在サポートされている RDMA テクノロジは次のとおりです。

-   Infiniband (IB)
-   インターネットワイドエリア RDMA プロトコル (iWARP)
-   RDMA over 収束イーサネット (RoCE)

RDMA、Infiniband、iWARP、RoCE の詳細については、次のリソースを参照してください。

-   [RFC 5040: リモートダイレクトメモリアクセスプロトコルの仕様](https://tools.ietf.org/html/rfc5040)
-   [RFC 5041: Reliable トランスポートを介したデータの直接配置](https://tools.ietf.org/html/rfc5041)
-   [RFC 5042: Direct Data Placement Protocol (DDP)/リモートダイレクトメモリアクセスプロトコル (RDMAP) のセキュリティ](https://tools.ietf.org/html/rfc5042)
-   [RFC 5043: ストリーム制御伝送プロトコル (SCTP) の直接データ配置 (DDP) の適応](https://tools.ietf.org/html/rfc5043)
-   [RFC 5044: マーカー PDU Aligned フレーミング (TCP 仕様用)](https://tools.ietf.org/html/rfc5044)
-   [RDMA コンソーシアム](https://www.rdmaconsortium.org/)
-   [インターネットドラフト: RDMA プロトコル動詞仕様](https://tools.ietf.org/html/draft-hilland-rddp-verbs-00)
-   [Infiniband 取引の関連付け (Infiniband と RoCE のダウンロード可能な仕様用)](https://www.infinibandta.org/)

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 







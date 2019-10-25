---
title: NDPROXY の概要
description: NDPROXY の概要
ms.assetid: 98d01249-8a6d-42b3-a91c-811352c8b638
keywords:
- NDPROXY WDK ネットワーク
- NDISWAN WDK ネットワーク
- アーキテクチャ WDK WAN、NDPROXY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae77a667a7eb68af84d84e25c13e461aabd4568e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829095"
---
# <a name="ndproxy-overview"></a>NDPROXY の概要





**注**  このページを読んでいる場合は、windows XP と windows Server 2003 に影響する、2013年11月の[マイクロソフトセキュリティアドバイザリ (2914486)](https://docs.microsoft.com/security-updates/SecurityAdvisories/2014/2914486)が原因で、この信頼できるコンピューティングの[ブログ投稿](https://blogs.technet.microsoft.com/msrc/2013/11/27/microsoft-releases-security-advisory-2914486/)が役に立つことがあります。

 

NDPROXY は、NDISWAN と CoNDIS WAN ドライバー (WAN ミニポートドライバー、コールマネージャー、およびミニポートコールマネージャー) を TAPI サービスにインターフェイスするシステム提供のドライバーです。 このトピックでは、[電話 Services をサポートする CONDIS WAN 操作](condis-wan-operations-that-support-telephonic-services.md)で詳細に説明されている ndproxy 操作について説明します。

次の図は、RAS アーキテクチャの他のコンポーネントと NDPROXY のインターフェイスを示しています。

![ras アーキテクチャの他のコンポーネントと ndproxy のインターフェイスを示す図](images/ndproxy.png)

NDPROXY には、CoNDIS WAN 用の service provider interface (SPI) のカーネルモードコンポーネントが用意されています。 TAPI 対応アプリケーションは、ユーザーモードの TAPI 要求を行い、TAPI サービスはこれらの要求を NDPTSP にルーティングします。 NDPTSP は、ユーザーモードの TAPI サービス要求をカーネルモードの SPI 要求に変換し、その SPI 要求を NDPROXY に渡します。

NDPROXY は、NDISWAN ドライバーと、次のいずれかの方法で NDIS を介して通信します。

-   別のコールマネージャーがあるミニポートドライバー

-   Integrated ミニポート呼び出しマネージャー (MCM)

構成に関係なく、NDISWAN と NDPROXY に対するミニポートドライバーインターフェイスとコールマネージャーインターフェイスは同じです。

複数のハードウェアプラットフォームをサポートする必要がある場合は、別の呼び出しマネージャーでミニポートドライバーを使用でき  ことに**注意**してください。 このような状況では、同じコールマネージャーを複数のミニポートドライバーと組み合わせて使用して、開発を簡素化できます。

 

次の一覧は、NDPROXY と、CoNDIS WAN ドライバースタック内の他のコンポーネントとの間に存在するインターフェイスの概要を示しています。

-   NDPROXY は、接続指向のクライアントインターフェイスを提供し、WAN ミニポートドライバーと、NDISWAN へのコールマネージャーインターフェイスを提供します。

-   NDISWAN は、NDPROXY、CoNDIS WAN ミニポートドライバー、および MCMs への接続指向クライアントインターフェイスを提供します。

-   CoNDIS WAN 呼び出しマネージャーまたは MCMs は、NDPROXY にコールマネージャーインターフェイスを提供します。

-   CoNDIS WAN ミニポートドライバーおよび MCMs には、NDISWAN への condis ミニポートドライバーインターフェイスが存在します。

接続指向クライアント、通話マネージャー、ミニポートドライバー、および MCMs の詳細については、「[接続指向環境](connection-oriented-environment.md)」を参照してください。

NDPROXY は、接続指向の TAPI Oid を使用して[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出し、CONDIS WAN ミニポートドライバーの機能を決定します。 また、NDPROXY は、TAPI 固有のアドレスファミリを登録し、仮想接続 (VCs) を作成し、呼び出しを許可して、VCs をアクティブ化して、それらの VCs でデータを送受信できるようにします。 CoNDIS WAN ミニポートドライバーでの OID 要求の処理の詳細については、「condis wan ミニポート[ドライバーでのクエリの処理](handling-queries-in-a-condis-wan-miniport-driver.md)」および「 [Condis Wan ミニポートドライバー情報の設定](setting-condis-wan-miniport-driver-information.md)」を参照してください。

 

 






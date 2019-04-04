---
title: NDPROXY の概要
description: NDPROXY の概要
ms.assetid: 98d01249-8a6d-42b3-a91c-811352c8b638
keywords:
- ネットワーク NDPROXY WDK
- ネットワーク NDISWAN WDK
- アーキテクチャの WDK WAN NDPROXY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52f3297f318c6b7f7ad8beecb7059bd4400e7170
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570196"
---
# <a name="ndproxy-overview"></a>NDPROXY の概要





**注**  27 の 2013 年 11 月のため、このページを読んでいるかどうかは[マイクロソフト セキュリティ アドバイザリ (2914486)](https://technet.microsoft.com/security/advisory/2914486) Windows XP および Windows Server 2003 に影響を与えることがありますこの信頼できるコンピューティング[ブログの投稿](http://blogs.technet.com/b/msrc/archive/2013/11/27/microsoft-releases-security-advisory-2914486.aspx)に役立ちます。

 

NDPROXY は、システム指定のドライバーで、TAPI サービスへの NDISWAN およびいる CoNDIS WAN ドライバー (WAN ミニポート ドライバー、コール マネージャー、およびミニポート コール マネージャー) のインターフェイスです。 ここでさらに記載されている NDPROXY 操作[いる CoNDIS WAN 操作電話サービスをサポートする](condis-wan-operations-that-support-telephonic-services.md)します。

次の図は、RAS アーキテクチャでは、他のコンポーネントと NDPROXY のインターフェイスを示します。

![ndproxy が ras アーキテクチャの他のコンポーネントとやり取りする方法を示す図](images/ndproxy.png)

NDPROXY いる CoNDIS WAN のサービス プロバイダー インターフェイス (SPI) のカーネル モード コンポーネントを提供します。 TAPI 対応のアプリケーションはユーザー モードの TAPI 要求を行い、TAPI サービスが NDPTSP にこれらの要求をルーティングします。 NDPTSP では、カーネル モードの SPI の要求とパス、SPI を NDPROXY を要求するユーザー モードの TAPI サービス要求に変換します。

NDPROXY は、次のいずれかの NDISWAN ドライバーと NDIS を通じて通信します。

-   ミニポート ドライバーを個別に呼び出してマネージャー

-   統合のミニポート マネージャー (MCM) を呼び出す

ミニポート ドライバー インターフェイスと NDISWAN を NDPROXY マネージャー インターフェイスの呼び出しは、構成に関係なく同じです。

**注**  を別個の呼び出しのマネージャーで複数のハードウェア プラットフォームをサポートする必要がある場合、ミニポート ドライバーを使用することができます。 このような状況では、同じコール マネージャーは開発を簡略化の複数のミニポート ドライバーと組み合わせて使用できます。

 

NDPROXY と WAN いる CoNDIS ドライバー スタックの他のコンポーネント間に存在するインターフェイスを次に示します。

-   NDPROXY いる CoNDIS WAN ミニポート ドライバー インターフェイスと NDISWAN にコール マネージャー インターフェイス、接続指向のクライアントを表示します。

-   NDISWAN NDPROXY、するクライアントの接続指向のインターフェイスを表示しましている CoNDIS WAN ミニポート ドライバー、および MCMs します。

-   いる CoNDIS WAN のコール マネージャーまたは MCMs は、NDPROXY にコール マネージャー インターフェイスを提供します。

-   いる CoNDIS WAN ミニポート ドライバーと MCMs は、NDISWAN にいる CoNDIS ミニポート ドライバー インターフェイスを提供します。

クライアントの接続指向、コール マネージャー、ミニポート ドライバー、および MCMs の詳細については、[Connection-Oriented 環境](connection-oriented-environment.md)を参照してください。

NDPROXY 呼び出し、 [ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)接続指向の TAPI Oid いる CoNDIS WAN ミニポート ドライバーの機能を決定する関数。 NDPROXY も TAPI に固有のアドレス ファミリを登録、仮想接続 (VCs) を作成します、によりし、呼び出しを受け入れますおよびデータを送信して、それらの VCs で受信したように、VCs をアクティブにします。 いる CoNDIS WAN ミニポート ドライバーで OID 要求の処理の詳細については、[いる CoNDIS WAN ミニポート ドライバーで処理クエリ](handling-queries-in-a-condis-wan-miniport-driver.md)と[設定いる CoNDIS WAN ミニポート ドライバー情報](setting-condis-wan-miniport-driver-information.md)を参照してください。

 

 






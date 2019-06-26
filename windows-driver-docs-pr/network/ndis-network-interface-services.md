---
title: NDIS ネットワーク インターフェイス サービス
description: NDIS ネットワーク インターフェイス サービス
ms.assetid: c37d9b7e-bc56-41e6-b41f-92a6df890e8e
keywords:
- NDIS インターフェイス WDK、サービスをネットワークします。
- ネットワーク インターフェイスの WDK、サービス
- WDK のサービスのネットワーク インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1439e42039e24b590efc22b4c7ca80fc72031db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354977"
---
# <a name="ndis-network-interface-services"></a>NDIS ネットワーク インターフェイス サービス





NDIS のネットワーク インターフェイスのプログラミング インターフェイスがサービスを提供します。

-   ローカル一意識別子を生成 ( [ **NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)) の各インターフェイス。 NET\_LUID 値。
    -   コンピューターを再起動するとを保持する必要があります。 プロバイダーのインターフェイスは、NET を行う必要があります\_関連付けられているインターフェイスが永続的でない場合でも永続的な Luid。 たとえば、この永続化は、NET を解放するインターフェイス プロバイダーを使用できます。\_LUID インデックス コンピューターの電源障害がある場合。
    -   インターフェイス型に関連付けられている必要があります ( *IfType*で RFC 2863)。
    -   ローカル コンピューター上で一意である必要があります。
    -   のテキスト表現に変換できる、NET\_LUID は、インターフェイス名と同じです (*もし Name*で RFC 2863)。
-   ローカルで一意のインターフェイス インデックスを生成する (24 ビットの値としても参照されている*IfIndex* ) の各インターフェイス。 *IfIndex*値の次のプロパティがあります。
    -   小さい数値は、適しています。 たとえば、NDIS は、最小の利用可能なインターフェイスのインデックスを再利用します。
    -   *IfIndex*コンピューターを再起動すると、値が保持されません。
    -   一対一の対応関係がある、 [ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値と*IfIndex*値。
-   インターフェイスのインデックス、NET 間のマップ\_LUID 値、および「表示名」(たとえば、ネットワーク接続 フォルダーに表示されるフレンドリ名)。

-   ドライバー スタックでは、インターフェイスの重ね順を定義します。

-   クエリを実行し、NDIS ドライバーを管理し、その Rfc 2863 と 2864 を指定するインターフェイスのプロパティとテーブルを設定します。

 

 






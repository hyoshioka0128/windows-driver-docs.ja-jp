---
title: 逆シリアル化された NDIS ミニポート ドライバー
description: 逆シリアル化された NDIS ミニポート ドライバー
ms.assetid: d133370a-48f4-425b-a2bd-d95ec8b5c369
keywords:
- ミニポート ドライバー WDK ネットワークの種類
- NDIS ミニポート ドライバー WDK、種類
- 逆シリアル化された NDIS ミニポート ドライバー WDK ネットワーク
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: f9c3cf06239430cbb30659b38ffcf3202913a673
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381434"
---
# <a name="deserialized-ndis-miniport-drivers"></a>逆シリアル化された NDIS ミニポート ドライバー





すべての NDIS 6.0 とそれ以降のドライバーが*逆シリアル化*します。

A*逆シリアル化された NDIS ミニポート ドライバー* 、独自の操作をシリアル化*MiniportXxx*関数し内部的にすべての送信要求をキューではなくこれらの関数を実行する NDIS に依存します。 その結果、逆シリアル化されたミニポート ドライバーでは、シリアル化されたミニポート ドライバーよりも、全二重パフォーマンスが大幅に向上を実現できます。

逆シリアル化されたドライバー モデルは、NDIS ミニポート ドライバーの既定のモデルです。 接続指向のミニポート ドライバー、ミニポート ドライバー WDM 下端がほかには、逆シリアル化されたドライバーがある場合があります。 新しい NDIS ミニポート ドライバーを記述する場合は、逆シリアル化されたドライバーを記述する必要があります。 可能であれば、する必要がありますもポート古いドライバー NDIS 6.0 以降。 移植のドライバーの詳細についてを参照してください。

-   [NDIS 6.0 への移植の NDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
-   [NDIS 6.20 が動作する移植の NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-20.md)
-   [NDIS 6.30 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-30.md)

NDIS とのインターフェイス、ときに、逆シリアル化されたミニポート ドライバーは、次の要件を満たす必要があります。

-   逆シリアル化されたミニポート ドライバーに自らをよう NDIS の初期化中にします。

-   逆シリアル化されたミニポート ドライバーでは、すべての送信要求を非同期的に実行する必要があります。 コネクションレスの NDIS 6.0 とそれ以降のミニポート ドライバーを呼び出す送信要求を完了する、 **NdisMSendNetBufferListsComplete**関数。 NDIS 6.0 の接続指向と呼び出し後のミニポート ドライバー、 **NdisMCoSendNetBufferListsComplete**関数。

-   NDIS 6.0 またはそれ以降のセットをサポートする逆シリアル化されたミニポート ドライバー、**状態**net メンバー\_バッファー\_リスト構造に渡すこと**NdisMSendNetBufferListsComplete**.

-   場合は、逆シリアル化されたミニポート ドライバーでは、完全な送信要求の直前にことはできません、requeuing の要求を NDIS に返すことはできませんに。 代わりに、データを送信するための十分なリソースが利用されるまで、ミニポート ドライバーで内部的に要求を送信する必要がありますキュー。

-   逆シリアル化されたミニポート ドライバーが NDIS に渡される構造を調べる必要がありますいないで後に表示されるまでの兆候 NDIS は、それらを返します。 NDIS 返します NET\_バッファー\_ミニポート ドライバーのリストの構造体*MiniportReturnNetBufferLists*関数。

逆シリアル化されたミニポート ドライバーでは、次のドライバー内部の要件を満たす必要があります。

-   逆シリアル化されたミニポート ドライバーでのネットワーク バッファー キューを保護する必要があります[スピンロック](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-spin-locks)します。 逆シリアル化されたミニポート ドライバーはそれ自体で同時にアクセスの共有状態も保護する必要があります*MiniportXxx*関数。

-   逆シリアル化されたミニポート ドライバーの*MiniportXxx* IRQL で関数が実行できる&lt;= ディスパッチ\_レベル。 その結果、ドライバーの作成者とは限りませんを*MiniportXxx*要求を処理する、シーケンス内の関数が呼び出されます。 1 つ*MiniportXxx*関数が別にプリエンプト*MiniportXxx*低い IRQL でを実行する関数。

-   逆シリアル化されたミニポート ドライバーでは、ネットワーク バッファー キューの管理を担当します。 ミニポート ドライバーにリソースの問題が発生した場合は、requeuing の NDIS に送信要求を戻ることことはできません。 代わりに、ミニポート ドライバーは、データを送信するための十分なリソースが利用されるまで、内部的にすべての送信要求をキューする必要があります。

-   逆シリアル化されたミニポート ドライバーには、プロトコルが指定した順序で送信要求を完了する必要があります。

送信し、受信 NDIS ドライバーの要件についての詳細についてを参照してください。[送信および受信操作](send-and-receive-operations.md)します。

逆シリアル化されたミニポート ドライバーが完了すると、通常、メモは、プロトコルが指定した順序で要求を送信します。 ただし、パケットの優先順位 (たとえば、IEEE 802.1 p) をサポートしているミニポート ドライバーでは、優先度の情報に基づいて、送信要求を並べ替えることができます。

 

 






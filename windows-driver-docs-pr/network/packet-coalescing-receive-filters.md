---
title: パケット結合受信フィルター
description: パケット結合受信フィルター
ms.assetid: B5C17A9D-A495-4A3D-B53E-B10F53C732D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9c4c66330163114f689af403550fab6a023039
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378662"
---
#  <a name="packet-coalescing-receive-filters"></a>パケット結合受信フィルター


NDIS 6.30、以降[NDIS 受信フィルター](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)パケットの結合をサポートするために拡張されています。 パケットの結合の場合は、各受信フィルターでは、次の項目を定義します。

-   ユーザー データグラム プロトコル (UDP) ヘッダーのメディア アクセス制御 (MAC) のヘッダーまたは転送先ポートの送信先アドレスなどのパケットのさまざまなプロトコル ヘッダー内のフィールドのセット。

-   合体受信フィルターに一致するパケットがネットワーク アダプターによって結合された最大時間。 アダプターでは、この値を使用して、アダプターのハードウェアのタイマーの有効期限値の設定。 タイマーが満了するとすぐに、アダプターは、ミニポート ドライバーは、結合されたパケットを処理できるように、ホストを中断する必要があります。

    **注**  受信フィルターに一致する最初のパケットを結合すると、タイマーが起動、ネットワーク アダプターをリセットして、タイマーを再起動することがなく受信フィルターに一致する追加のパケットを結合する必要があります。

     

ドライバーは、プロトコルとフィルター ドライバーなどの後続パケット結合ダウンロード受信ミニポート ドライバーにフィルターのオブジェクト識別子 (OID) のセット要求を発行して[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 詳細については、次を参照してください。[パケット結合受信フィルターの設定](setting-packet-coalescing-receive-filters.md)します。

ドライバーの後続パケット結合クエリを受け取ることもフィルター ミニポート ドライバーをダウンロードします。 上にあるドライバーでは、これを行うの OID メソッド要求を発行して[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)ミニポート ドライバーにします。 詳細については、次を参照してください。[クエリを実行するパケット結合受信フィルター](querying-packet-coalescing-receive-filters.md)します。

 

 






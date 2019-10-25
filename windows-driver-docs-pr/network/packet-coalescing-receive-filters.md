---
title: パケット結合受信フィルター
description: パケット結合受信フィルター
ms.assetid: B5C17A9D-A495-4A3D-B53E-B10F53C732D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 202b0cb15a76efe286058b3106b3c76ae2c36cda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843719"
---
#  <a name="packet-coalescing-receive-filters"></a>パケット結合受信フィルター


NDIS 6.30 以降では、パケット合体をサポートするために[ndis 受信フィルター](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)が拡張されています。 パケット合体の受信フィルターはそれぞれ、次のものを定義します。

-   パケットのさまざまなプロトコルヘッダー内のフィールドのセット。たとえば、メディアアクセスコントロール (MAC) ヘッダーの宛先アドレスや、ユーザーデータグラムプロトコル (UDP) ヘッダーの宛先ポートなどです。

-   結合受信フィルターに一致するパケットがネットワークアダプターによって結合される最大時間。 アダプターは、この値を使用して、アダプターのハードウェアタイマーの有効期限の値を設定します。 タイマーが期限切れになると、アダプターはホストを中断して、ミニポートドライバーが結合されたパケットを処理できるようにする必要があります。

    受信フィルターに一致する最初のパケットが結合され、タイマーが開始されるとすぐに、ネットワークアダプターは、タイマーをリセットしたり再起動したりせずに、受信フィルターに一致する追加のパケットを結合する必要があります **。  **

     

プロトコルやフィルタードライバーなどのその他のドライバーでは、オブジェクト識別子 (OID) セットの Oid 要求を発行することによって、ミニポートドライバーにパケット合体受信フィルターをダウンロードします。これにより、 [\_フィルター\_設定された\_受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)を適用します。 詳細については、「[パケット合体受信フィルターの設定](setting-packet-coalescing-receive-filters.md)」を参照してください。

それまでのドライバーは、ミニポートドライバーにダウンロードされたパケット合体受信フィルターを照会することもできます。 これを行うには、oid の OID メソッド要求を発行して、 [\_列挙型\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)をミニポートドライバーに受信\_フィルターを\_します。 詳細については、「[パケット合体受信フィルターのクエリ](querying-packet-coalescing-receive-filters.md)」を参照してください。

 

 






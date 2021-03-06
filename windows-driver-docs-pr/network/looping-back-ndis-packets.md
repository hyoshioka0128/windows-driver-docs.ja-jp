---
title: NDIS パケットのループ バック
description: NDIS パケットのループ バック
ms.assetid: 85967cd6-6945-46d1-8872-7b000689b6db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789a48a014ffdacff361b46a50ae82d90affef8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356211"
---
# <a name="looping-back-ndis-packets"></a>NDIS パケットのループ バック





場合は、NDIS\_NBL\_フラグ\_IS\_ループバック\_パケット フラグ、 **NblFlags**のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造が設定されている、パケットはループバック パケット。 プロトコルおよびフィルター ドライバーは、パケットがループバック パケットであるかを判断するには、このフラグを確認できます。

NDIS は、すべての次の 3 つの条件が満たされている場合、パケットをループします。

1.  メディアの種類が、基になるミニポート アダプター **NdisMedium802\_3**または**NdisMedium802\_5**します。

2.  次の 3 つの条件のいずれかが満たされています。
    1.  プロトコル バインディング設定、NDIS\_パケット\_型\_無作為検出の設定で、 [OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)OID のパケット フィルターを指定する (および、Windows 8 以降、NDIS を設定しなかった\_パケット\_型\_なし\_同じ OID にローカル) と同じ場合、次のいずれかです。

        -   ミニポート アダプタには、複数のバインドがあります。
        -   ミニポート アダプタに接続されているフィルター モジュールがあるし、フィルター モジュールが、受信ハンドラーを登録します。

    2.  プロトコル バインディング設定、NDIS\_パケット\_型\_すべて\_でローカルの設定、 [OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)のパケット フィルターと、次のいずれかを指定する OID は true。
        -   ミニポート アダプタには、複数のバインドがあります。
        -   ミニポート アダプタに接続されているフィルター モジュールがあるし、フィルター モジュールが、受信ハンドラーを登録します。

    3.  呼び出し元の設定、NDIS\_送信\_フラグ\_確認\_の\_でループバック フラグ、 *SendFlags*のパラメーター、 [ **NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)関数。

3.  パケットが許容されるは、パケット フィルターを使用して設定によって決定される、 [OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)ミニポート アダプターの OID。 例を次に示します。
    -   パケットが直接パケットの場合は、パケットの宛先アドレスは、ミニポート アダプタの MAC アドレスと一致する必要があります。
    -   パケットがマルチキャスト パケットの場合は、パケット フィルターは NDIS をいる必要があります\_パケット\_型\_すべて\_マルチキャスト セットまたは送信先アドレスと一致するマルチキャスト アドレスのいずれかのミニポート アダプターのマルチキャストでアドレスの一覧と、パケット フィルターは NDIS\_パケット\_型\_マルチキャストのセット。
    -   パケットがブロードキャスト パケットの場合は、ミニポート アダプターのパケット フィルターは NDIS をいる必要があります\_パケット\_型\_ブロードキャストのセット。
    -   ミニポート アダプタのパケット フィルターは NDIS\_パケット\_型\_PROMISCUOUS または NDIS\_パケット\_型\_すべて\_ローカル セット。

プロトコル バインドでは、次のいずれかが true の場合、ループバック パケットを受け取ります。

1.  プロトコルのバインドは、NDIS、パケットの元の送信者\_送信\_フラグ\_確認\_の\_ループバックが設定されます。

2.  プロトコルのバインドが NDIS を設定していない\_パケット\_型\_いいえ\_パケット フィルターはローカルです。

次のいずれかに当てはまる場合、プロトコル バインドは、ループバック パケットを受信しません。

1.  プロトコル バインド設定 NDIS\_パケット\_型\_いいえ\_パケット フィルターし、ローカルがパケットの場合、元の送信者ではありません。

2.  プロトコルのバインドは、元の送信者が NDIS\_送信\_フラグ\_確認\_の\_ループバックが設定されていない、 *SendFlags* への呼び出しでパラメーター[**NdisSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissendnetbufferlists)関数。

次の図は、ループバック アルゴリズムのロジック フローを示しています。

![ループバック アルゴリズムのロジック フローを示すフローチャート](images/loopback.png)

 

 






---
title: NDIS パケットのループ バック
description: NDIS パケットのループ バック
ms.assetid: 85967cd6-6945-46d1-8872-7b000689b6db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60ea3a48e62577669508551cd1bfc92a65e842b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844141"
---
# <a name="looping-back-ndis-packets"></a>NDIS パケットのループ バック





NDIS\_NBL\_FLAGS\_が\_ループバック\_、 [**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の**nblflags**メンバーのパケットフラグが設定されていると、パケットはループバックパケットになります。 プロトコルドライバーとフィルタードライバーは、パケットがループバックパケットであるかどうかを確認するために、このフラグをチェックします。

次の3つの条件がすべて満たされた場合、NDIS はパケットをループバックします。

1.  基になるミニポートアダプターメディアの種類は、 **NdisMedium802\_3**または**NdisMedium802\_5**です。

2.  次の3つの条件のいずれかが満たされています。
    1.  プロトコルバインドでは、NDIS\_PACKET\_TYPE\_プロミスカス設定を[oid\_GEN\_現在の\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter) oid で設定し、パケットフィルターを指定します (および Windows 8 以降の場合)。では、NDIS\_PACKET\_TYPE\_同じ OID 内に\_ローカル) が設定されておらず、次のいずれかが当てはまります。

        -   ミニポートアダプターに複数のバインドがあります。
        -   ミニポートアダプターにフィルターモジュールがアタッチされていて、フィルターモジュールによって受信ハンドラーが登録されています。

    2.  プロトコルバインドによって、NDIS\_PACKET\_TYPE\_すべての\_ローカル設定が[oid\_GEN\_現在の\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter) oid で設定されます。これにより、パケットフィルターが指定され、次のいずれかに該当します。
        -   ミニポートアダプターに複数のバインドがあります。
        -   ミニポートアダプターにフィルターモジュールがアタッチされていて、フィルターモジュールによって受信ハンドラーが登録されています。

    3.  呼び出し元は、 [**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数の*sendflags*パラメーターで\_ループバックフラグの\_を確認\_\_フラグを送信するように NDIS\_設定します。

3.  パケットフィルターセットによって設定されたパケットフィルターによって、ミニポートアダプターの[\_現在の\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter) oid が\_使用されている場合は、そのパケットが許容されます。 次に例をいくつか示します。
    -   パケットが直接パケットの場合は、パケットの宛先アドレスがミニポートアダプターの MAC アドレスと一致している必要があります。
    -   パケットがマルチキャストパケットの場合、パケットフィルターには、NDIS\_PACKET\_TYPE\_すべての\_マルチキャストセット、または宛先アドレスが、ミニポートアダプターのマルチキャストアドレス一覧のマルチキャストアドレスの1つと一致している必要があります。パケットフィルターには、NDIS\_パケット\_種類\_マルチキャストセットがあります。
    -   パケットがブロードキャストパケットの場合、ミニポートアダプターのパケットフィルターには、NDIS\_パケット\_種類\_ブロードキャストセットが必要です。
    -   ミニポートアダプターのパケットフィルターには、NDIS\_パケット\_タイプ\_無作為検出または NDIS\_パケット\_型\_すべて\_ローカルセットが含まれています。

次のいずれかに該当する場合、プロトコルバインドはループバックパケットを受信します。

1.  プロトコルバインドはパケットの元の送信側であり、NDIS\_送信\_フラグ\_チェック\_\_ループバックが設定されていることを確認します。

2.  プロトコルバインドでは、パケットフィルターに\_ローカルではなく、NDIS\_PACKET\_TYPE\_設定されません。

次のいずれかに該当する場合、プロトコルバインドはループバックパケットを受信しません。

1.  このプロトコルバインドでは、NDIS\_PACKET\_TYPE\_パケットフィルターにローカル\_が設定されておらず、パケットの元の送信者でもありません。

2.  プロトコルバインドは元の送信側です\_が、 [**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数の*呼び出しで、* \_ループバックの\_フラグ\_チェック\_を送信することはできません。

次の図は、ループバックアルゴリズムのロジックフローを示しています。

![ループバックアルゴリズムロジックフローを示すフローチャート](images/loopback.png)

 

 






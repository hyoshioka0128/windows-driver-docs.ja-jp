---
title: パケット結合受信フィルターの変更
description: パケット結合受信フィルターの変更
ms.assetid: 082A969F-2977-482A-B060-ED8D353EC2E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ab251b40c45205a493d65b1f105585b59387d31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382200"
---
# <a name="modifying-packet-coalescing-receive-filters"></a>パケット結合受信フィルターの変更


パケットの結合をサポートしているミニポート ドライバーに対する受信フィルターを変更するに、上位のプロトコルまたはフィルター ドライバーは、次の手順を実行します。

1.  上にあるドライバーがの OID メソッド要求を発行するミニポート ドライバーにダウンロードされているフィルターをすべての受信パケットの結合の一覧を取得する[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体。

    **注**上にあるドライバーまたはアプリケーションを初期化するときに、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)設定する必要があります、構造、 **QueueId** NDIS メンバー\_既定\_受信\_キュー\_id。

    OID メソッド要求から正常に戻った後[OID\_受信\_フィルター\_ENUM\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造には、更新されたへのポインターが含まれる[ **NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体が 1 つまたは複数続く[ **NDIS\_受信\_フィルター\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info)構造体。 各**NDIS\_受信\_フィルター\_情報**構造体は、ネットワーク アダプターに設定されているフィルターの識別子 (ID) を指定します。

2.  特定のパケットのパラメーターを取得する結合フィルターの上にあるドライバーの問題 OID メソッド要求のミニポート ドライバーにダウンロードされたを受信[OID\_受信\_フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters). **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。 上にあるドライバーまたはアプリケーションの初期化、 **NDIS\_受信\_フィルター\_パラメーター**構造体を設定して、 **FilterId**メンバーを 0 以外の IDパラメーターが返されるフィルターの値。

    OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体バッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

    -   [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) NDIS 受信フィルターのパラメーターを指定する構造体。

    -   配列の[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)フィルターを指定する構造体は、フィールドを 1 つの条件をテストします。ネットワーク パケットのヘッダー。

3.  上にあるドライバーは、追加、削除、またはテスト条件のフィルターのセットを変更するには、受信フィルターを変更します。 ドライバーは追加、削除、または個々 の変更によって[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)から構造体指定されたフィールド パラメーターの配列、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。

    メンバーを更新する必要があります、上にあるドライバーには、テスト条件への変更が完了したら、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)受信フィルターに加えられた変更を反映するように構造体。 たとえば、上にあるドライバーを更新する必要があります、 **FieldParametersArrayNumElements**メンバーを含む新しい配列の要素数。

    詳細については、次を参照してください。[パケット結合受信フィルターを指定する](specifying-a-packet-coalescing-receive-filter.md)します。

4.  上にあるドライバーの OID メソッド要求を発行する[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)ミニポート ドライバーに変更された受信フィルターをダウンロードします。

    詳細については、次を参照してください。[パケット結合受信フィルターを設定](setting-a-packet-coalescing-receive-filter.md)します。










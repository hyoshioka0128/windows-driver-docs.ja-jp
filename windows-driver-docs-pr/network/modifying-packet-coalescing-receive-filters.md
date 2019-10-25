---
title: パケット結合受信フィルターの変更
description: パケット結合受信フィルターの変更
ms.assetid: 082A969F-2977-482A-B060-ED8D353EC2E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76a39853622635ad84d7c63ca7ceb269b1c4fd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844223"
---
# <a name="modifying-packet-coalescing-receive-filters"></a>パケット結合受信フィルターの変更


パケット合体をサポートするミニポートドライバーで受信フィルターを変更するには、プロトコルまたはフィルタードライバーが次の手順を実行します。

1.  ミニポートドライバーにダウンロードされたすべてのパケット合体受信フィルターの一覧を取得するために、このドライバーは oid の OID メソッド要求を発行します。このフィルター [\_列挙\_フィルターを受け取る\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体へのポインターが含まれています。

    **メモ** 前のドライバーまたはアプリケーションが Ndis を初期化するときに、 [ **\_フィルター\_情報\_配列構造を受け取る\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array) 、 **QUEUEID**メンバーを NDIS\_DEFAULT\_receive\_QUEUE に設定する必要があり\_ID。

    Oid の OID メソッド要求から正常に返された後、 [ENUM\_フィルター\_列挙型フィルターを\_受け取る\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、更新された[**ndis\_へのポインター\_情報\_配列の構造を受け取る\_フィルターを取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)します。この後に1つ以上の ndis\_、\_[**フィルター\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)構造体を受け取ります。 各**NDIS\_受信\_フィルター\_情報**構造は、ネットワークアダプターに設定されているフィルターの識別子 (id) を指定します。

2.  ミニポートドライバーにダウンロードされた特定のパケット合体受信フィルターのパラメーターを取得するために、このドライバーは oid の oid メソッド要求を発行し、 [\_フィルター\_パラメーターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)ように\_します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。 前のドライバーまたはアプリケーションは、 **Filterid**メンバーを、パラメーターが返されるフィルターの0以外の id 値に設定することによって、 **NDIS\_受信\_フィルター\_パラメーター**構造を初期化します。

    OID メソッド要求から正常に戻った後、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

    -   Ndis\_は、NDIS 受信フィルターのパラメーターを指定する[ **\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を受け取ります。

    -   ネットワークパケットヘッダー内の1つのフィールドのフィルターテスト条件を指定する、 [ **\_フィルター\_フィールド\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)の配列。

3.  前のドライバーは、フィルターの一連のテスト条件を追加、削除、または変更するために受信フィルターを変更します。 これを行うには、ndis\_RECEIVE\_FILTER によって指定されたフィールドパラメーター配列から[ **\_フィルター\_フィールド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)構造を追加、削除、または\_変更することで、この処理を行い[ **@noパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)の構造。

    前のドライバーがテスト条件に対する変更を完了したら、受信フィルターに加えられた変更を反映するために、 [**NDIS\_受信\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造のメンバーを更新する必要があります。 たとえば、前のドライバーでは、配列内の新しい要素数を格納するように**FieldParametersArrayNumElements**メンバーを更新する必要があります。

    詳細については、「[パケット合体受信フィルターの指定](specifying-a-packet-coalescing-receive-filter.md)」を参照してください。

4.  この後のドライバーは、oid の OID メソッド要求を発行し[\_\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)を適用して、変更された受信フィルターをミニポートドライバーにダウンロードします。

    詳細については、「[パケット合体受信フィルターの設定](setting-a-packet-coalescing-receive-filter.md)」を参照してください。










---
title: パケット結合受信フィルターの設定
description: パケット結合受信フィルターの設定
ms.assetid: 59BD092F-A530-446F-93E7-02E1F254E9A0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe304bb8d8041e910dbd737e684fe6264856864c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841961"
---
# <a name="setting-a-packet-coalescing-receive-filter"></a>パケット結合受信フィルターの設定


パケット合体をサポートするミニポートドライバーに対して受信フィルターをダウンロードして設定するには、それ以降のドライバーは oid の OID メソッド要求を発行し[\_\_フィルター\_設定\_フィルターを設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 OID 要求の[ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   Ndis\_は、NDIS 受信フィルターのパラメーターを指定する[ **\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を受け取ります。

-   ネットワークパケットヘッダー内のフィールドのフィルターテスト条件を指定する、 [ **\_フィルター\_フィールド\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)の配列。

後続のドライバーでパケット合体受信フィルターのパラメーターを指定する方法の詳細については、「[パケット合体受信フィルターの指定](specifying-a-packet-coalescing-receive-filter.md)」を参照してください。

NDIS が基になるネットワークアダプターに対して受信フィルターを設定する OID 要求を受信すると、受信フィルターパラメーターが検証されます。 それまでのドライバーが新しい受信フィルターを指定している場合、NDIS は受信フィルターの一意のフィルター識別子 (ID) も生成します。

NDIS が必要なリソースとフィルター ID を割り当てると、OID 要求がミニポートドライバーに転送されます。 ミニポートドライバーが受信フィルターに必要なソフトウェアリソースとハードウェアリソースを正常に割り当てることができる場合、ミニポートドライバーは、NDIS\_STATUS\_SUCCESS の状態で OID 要求を完了します。

Oid の OID メソッド要求から正常に返された後[\_フィルター\_設定された\_受信\_フィルターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)と、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーにポインターが含まれます。[**NDIS\_受信\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。 この構造は、新しいフィルター ID で NDIS によって更新されます。

 

 






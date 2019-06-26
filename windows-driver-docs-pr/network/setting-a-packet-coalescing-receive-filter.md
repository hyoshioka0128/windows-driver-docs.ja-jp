---
title: パケット結合受信フィルターの設定
description: パケット結合受信フィルターの設定
ms.assetid: 59BD092F-A530-446F-93E7-02E1F254E9A0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d3b15629976c392c4a87cb1535a2c5f2963830f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386830"
---
# <a name="setting-a-packet-coalescing-receive-filter"></a>パケット結合受信フィルターの設定


OID メソッド要求を発行している上位のドライバーをダウンロードして、パケットの結合をサポートしているミニポート ドライバーに対して受信フィルターを設定、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter). **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID 要求へのポインターが含まれている構造体、呼び出し元が割り当てたバッファー。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) NDIS のパラメーターを指定する構造体は、フィルターを受信します。

-   配列の[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)フィルターを指定する構造体のフィールドの条件をテストします。ネットワーク パケットのヘッダー。

上位のドライバーがパラメーターを指定するフィルターを受信パケットの結合の方法の詳細については、次を参照してください。[パケット結合受信フィルターを指定する](specifying-a-packet-coalescing-receive-filter.md)します。

NDIS は、基になるネットワーク アダプターで受信フィルターを設定する OID 要求を受信、受信のフィルター パラメーターを確認します。 上にあるドライバーは、新しい受信フィルターを指定する場合は、NDIS 受信フィルターのフィルターの一意な識別子 (ID) も生成されます。

NDIS は、必要なリソースや、フィルター ID に割り当てます後、に、ミニポート ドライバーに OID 要求を転送します。 ミニポート ドライバーが NDIS の状態で OID 要求を完了する場合は、ミニポート ドライバーは、受信フィルターを必要なソフトウェアとハードウェア リソースを割り当てることができますが正常に、\_状態\_成功します。

OID メソッド要求から正常に戻った後[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)、 **InformationBuffer**のメンバー、[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体。 この構造体は、新しいフィルター ID に置き換えます。 NDIS によって更新されます。

 

 






---
title: 64 ビット統計情報 OID のクエリ
description: 64 ビット統計情報 OID のクエリ
ms.assetid: dc43c33d-12a7-4468-9980-a9015f43e068
keywords:
- Oid の WDK ネットワークの統計情報
- 64 ビットの統計情報の Oid WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 046de3820940786890ec595a88ad3bc2253c241b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385445"
---
# <a name="querying-64-bit-statistics-oids"></a>64 ビット統計情報 OID のクエリ


カウンター特定の Oid の統計情報のすべてのミニポート ドライバーを/秒 (Gbps) の 1 ギガバイトは、高速化、64 ビットをサポートする必要があります。 すべての 100 メガバイト/秒 (Mbps) より高速のミニポート ドライバーでは、このような Oid の 64 ビットのカウンターをサポートする必要があります。 コネクションレスのミニポート ドライバーの統計の Oid の詳細については、次を参照してください。 [General Statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)します。 接続指向のミニポート ドライバーには、このような Oid の詳細については、次を参照してください。 [Connection-Oriented ミニポート ドライバーの全般的な統計](https://docs.microsoft.com/windows-hardware/drivers/network/general-statistics-oids-for-connection-oriented-miniport-drivers)します。

OID の統計情報のクエリを実行する要求元の設定 NDIS\_OID\_要求**InformationBufferLength** 4 (バイト単位) を 32 ビットの統計情報要求を示すために、64 ビットの統計情報要求を示す 8 (バイト単位)。 応答に、ミニポート ドライバー設定 NDIS\_OID\_要求**BytesNeeded**ミニポート ドライバーでは、64 ビット (4 は、32 ビット) または 8 をサポートする統計値のサイズにします。 ミニポート ドライバー設定 NDIS\_OID\_要求**BytesWritten**小さい方の**InformationBufferLength**値と統計情報のサイズをミニポート ドライバーサポートされています。

次のセクションでは、64 ビットの統計情報の Oid をサポートしているミニポート ドライバーがこのような Oid のクエリに応答する方法について説明します。

### <a href="" id="-64-bit-query-of-a-64-bit-value"></a>64 ビット値の 64 ビットのクエリ

NDIS\_OID\_要求**InformationBufferLength**が 8 以上。

ミニポート ドライバー:

-   情報バッファー内には、64 ビット値を返します。

-   NDIS 設定\_OID\_要求**BytesWritten** 8。

-   NDIS 返します\_状態\_成功からその[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)または[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数。

### <a href="" id="-32-bit-query-of-a-64-bit-value"></a>64 ビット値の 32 ビットのクエリ

NDIS\_OID\_要求**InformationBufferLength**に大きい以上 4 および 8 未満にします。

ミニポート ドライバー:

-   情報のバッファー、64 ビット値の下位 32 ビットで返します。

-   NDIS 設定\_OID\_要求**BytesWritten** 4 にします。

-   NDIS 設定\_OID\_要求**BytesNeeded** 8。

-   NDIS 返します\_状態\_成功からその[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)または[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数。

### <a name="invalid-length-query-of-a-64-bit-value"></a>64 ビット値の無効な長さのクエリ

NDIS\_OID\_要求**InformationBufferLength**は 4 未満です。

ミニポート ドライバー:

-   情報バッファーでは、任意の値は返されません。

-   NDIS 設定\_OID\_要求**BytesWritten**を 0 にします。

-   NDIS 設定\_OID\_要求**BytesNeeded** 8。

-   NDIS 返します\_状態\_無効な\_から長さその[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)または[ **MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数。

 

 






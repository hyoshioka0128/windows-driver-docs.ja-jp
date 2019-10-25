---
title: 64 ビット統計情報 OID のクエリ
description: 64 ビット統計情報 OID のクエリ
ms.assetid: dc43c33d-12a7-4468-9980-a9015f43e068
keywords:
- 統計 Oid WDK ネットワーク
- 64ビット統計 Oid WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fd9342bd9af1165e841b40c5258482a894d0b6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844895"
---
# <a name="querying-64-bit-statistics-oids"></a>64 ビット統計情報 OID のクエリ


1ギガバイト/秒 (Gbps) 以降のすべてのミニポートドライバーは、特定の統計 Oid の64ビットカウンターをサポートする必要があります。 100 Mb/秒 (Mbps) 以上の高速ミニポートドライバーは、このような Oid に対して64ビットのカウンターをサポートする必要があります。 コネクションレスミニポートドライバーの統計 Oid の詳細については、「 [General statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)」を参照してください。 接続指向ミニポートドライバーのそのような Oid の詳細については、「[接続指向ミニポートドライバーの一般的な統計](https://docs.microsoft.com/windows-hardware/drivers/network/general-statistics-oids-for-connection-oriented-miniport-drivers)」を参照してください。

統計の OID を照会する要求元は、NDIS\_OID を設定\_要求**Informationbufferlength**を 4 (バイト) に設定して32ビットの統計情報要求を示すか、8 (バイト) を64ビットの統計情報の要求を示します。 応答では、ミニポートドライバーによって、ミニポートドライバーがサポートしている統計値のサイズ (32 ビットの場合は4、64ビットの場合は 8) **\_要求の\_OID が設定**されます。 ミニポートドライバーは、データ**バッファーの長さ**の値の小さい方とミニポートドライバーがサポートする統計のサイズに対して書き込まれた NDIS\_OID\_要求**byteswritten**設定します。

以下のセクションでは、64ビット統計 Oid をサポートするミニポートドライバーが、このような Oid のクエリにどのように応答するかについて説明します。

### <a href="" id="-64-bit-query-of-a-64-bit-value"></a>64ビット値の64ビットクエリ

NDIS\_OID\_REQUEST **Informationbufferlength**が8以上です。

ミニポートドライバー:

-   情報バッファー内の64ビット値を返します。

-   NDIS\_OID\_要求**byteswritten** 8 に書き込みます。

-   [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)または[**MINIPORTCOOIDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数から NDIS\_STATUS\_SUCCESS を返します。

### <a href="" id="-32-bit-query-of-a-64-bit-value"></a>64ビット値の32ビットクエリ

NDIS\_OID\_要求情報**Bufferlength**が4以上で8未満です。

ミニポートドライバー:

-   情報バッファー内の64ビット値の下位32ビットを返します。

-   NDIS\_OID\_要求**byteswritten** 4 に書き込みます。

-   NDIS\_OID\_要求**bytesneeded** 8 に設定します。

-   [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)または[**MINIPORTCOOIDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数から NDIS\_STATUS\_SUCCESS を返します。

### <a name="invalid-length-query-of-a-64-bit-value"></a>64ビット値の無効な長さのクエリ

NDIS\_OID\_要求情報**Bufferlength**が4未満です。

ミニポートドライバー:

-   は、情報バッファーに値を返しません。

-   NDIS\_OID を0に**書き込み**\_要求するように設定します。

-   NDIS\_OID\_要求**bytesneeded** 8 に設定します。

-   は、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)または[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数からの無効な\_の長さ\_NDIS\_STATUS を返します。

 

 






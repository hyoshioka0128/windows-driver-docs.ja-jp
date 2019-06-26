---
title: 接続指向ミニポート ドライバーの一般統計情報 OID
description: このトピックでは、オブジェクトの接続指向の全般的な統計の Oid をについて説明します。
ms.assetid: 1967ebb9-0cc9-46ca-b9db-fc505f41c38e
keywords:
- 全般的な統計 Oid 接続指向のミニポート ドライバー
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9396f31f7c0ee7dacdc985f71147d1b1c4cd5da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382765"
---
# <a name="general-statistics-oids-for-connection-oriented-miniport-drivers"></a>接続指向ミニポート ドライバーの一般統計情報 OID

次の表は、接続指向のミニポート ドライバーの全般的な統計の特性や、Nic 設定を取得または使用 Oid をまとめたものです。

> [!TIP] 
> 接続指向のミニポート ドライバーでは、このような要求を処理するその[MiniportCoOidRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)コールバック関数。

次の表では、M は、OID は必須では、O は、これは省略可能なことを示しますを示します。

| 長さ | クエリ | Set | 名前 |
| --- | --- | --- | --- |
| 4 または 8 | O |   | [OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md) |
| 4 または 8 | O |   | [OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md) |
| 4 または 8 | O |   | [OID_GEN_CO_BYTES_XMIT_OUTSTANDING](oid-gen-co-bytes-xmit-outstanding.md) |
| 4 または 8 | O |   | [OID_GEN_CO_NETCARD_LOAD](oid-gen-co-netcard-load.md) |
| 4 または 8 | O |   | [OID_GEN_CO_RCV_CRC_ERROR](oid-gen-co-rcv-crc-error.md) |
| 4 または 8 | M |   | [OID_GEN_CO_RCV_PDUS_ERROR](oid-gen-co-rcv-pdus-error.md) |
| 4 または 8 | M |   | [OID_GEN_CO_RCV_PDUS_NO_BUFFER](oid-gen-co-rcv-pdus-no-buffer.md) |
| 4 または 8 | M |   | [OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md) |
| 4 または 8 | O |   | [OID_GEN_CO_TRANSMIT_QUEUE_LENGTH](oid-gen-co-transmit-queue-length.md) |
| 4 または 8 | M |   | [OID_GEN_CO_XMIT_PDUS_ERROR](oid-gen-co-xmit-pdus-error.md) |
| 4 または 8 | M |   | [OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md) |

## <a name="miniport-driver-support-for-64-bit-counters"></a>64 ビットのカウンターのミニポート ドライバーのサポート

すべての 1 Gbps、高速の接続指向のミニポート ドライバーは、以下の統計情報の Oid の 64 ビットのカウンターをサポートする必要があります。 さらに、Microsoft では、100 mbps と高速の接続指向 miiniport ドライバーをすべてが以下の統計情報の Oid の 64 ビットのカウンターをサポートをお勧めします。

[OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md)

[OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md)

[OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md)

[OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md)

このようなミニポート ドライバーでは、他の統計情報の送信を示すまたはエラーを受信する Oid などの Oid の 64 ビットのカウンターもサポートできます。

64 ビットのカウンターのシステムのサポートは、Windows XP およびそれ以降のバージョンで使用できます。


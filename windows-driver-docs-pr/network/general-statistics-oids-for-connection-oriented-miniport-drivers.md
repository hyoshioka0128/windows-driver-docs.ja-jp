---
title: 接続指向のミニポート ドライバーの全般的な統計の Oid
description: このトピックでは、オブジェクトの接続指向の全般的な統計の Oid をについて説明します。
ms.assetid: 1967ebb9-0cc9-46ca-b9db-fc505f41c38e
keywords:
- 全般的な統計 Oid 接続指向のミニポート ドライバー
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe516e58249a7654edf13c8777e60a03410e3327
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528320"
---
# <a name="general-statistics-oids-for-connection-oriented-miniport-drivers"></a>接続指向のミニポート ドライバーの全般的な統計の Oid

次の表は、接続指向のミニポート ドライバーの全般的な統計の特性や、Nic 設定を取得または使用 Oid をまとめたものです。

> [!TIP] 
> 接続指向のミニポート ドライバーでは、このような要求を処理するその[MiniportCoOidRequest](https://msdn.microsoft.com/library/windows/hardware/ff559362)コールバック関数。

次の表では、M は、OID は必須では、O は、これは省略可能なことを示しますを示します。

| 長さ | クエリ | 設定 | 名前 |
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


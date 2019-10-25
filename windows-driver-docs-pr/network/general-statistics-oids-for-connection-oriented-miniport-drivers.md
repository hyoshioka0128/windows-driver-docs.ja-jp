---
title: 接続指向ミニポート ドライバーの一般統計情報 OID
description: このトピックでは、接続指向オブジェクトの一般的な統計 Oid について説明します。
ms.assetid: 1967ebb9-0cc9-46ca-b9db-fc505f41c38e
keywords:
- 一般的な統計 Oid 接続指向ミニポートドライバー
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: aed8bc72c73eb155179e2dc3ab187aac1356430a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842186"
---
# <a name="general-statistics-oids-for-connection-oriented-miniport-drivers"></a>接続指向ミニポート ドライバーの一般統計情報 OID

次の表は、接続指向のミニポートドライバーや Nic の全般的な統計特性を取得または設定するために使用される Oid をまとめたものです。

> [!TIP] 
> 接続指向のミニポートドライバーは、そのような要求を[MiniportCoOidRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)コールバック関数で処理します。

この表では、M は OID が必須であることを示していますが、O は省略可能であることを示しています。

| 長さ | クエリ | 設定 | 名前 |
| --- | --- | --- | --- |
| 4または8 | O |   | [OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md) |
| 4または8 | O |   | [OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md) |
| 4または8 | O |   | [OID_GEN_CO_BYTES_XMIT_OUTSTANDING](oid-gen-co-bytes-xmit-outstanding.md) |
| 4または8 | O |   | [OID_GEN_CO_NETCARD_LOAD](oid-gen-co-netcard-load.md) |
| 4または8 | O |   | [OID_GEN_CO_RCV_CRC_ERROR](oid-gen-co-rcv-crc-error.md) |
| 4または8 | [M] |   | [OID_GEN_CO_RCV_PDUS_ERROR](oid-gen-co-rcv-pdus-error.md) |
| 4または8 | [M] |   | [OID_GEN_CO_RCV_PDUS_NO_BUFFER](oid-gen-co-rcv-pdus-no-buffer.md) |
| 4または8 | [M] |   | [OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md) |
| 4または8 | O |   | [OID_GEN_CO_TRANSMIT_QUEUE_LENGTH](oid-gen-co-transmit-queue-length.md) |
| 4または8 | [M] |   | [OID_GEN_CO_XMIT_PDUS_ERROR](oid-gen-co-xmit-pdus-error.md) |
| 4または8 | [M] |   | [OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md) |

## <a name="miniport-driver-support-for-64-bit-counters"></a>64ビットカウンターのミニポートドライバーのサポート

1 Gbps 以上の高速接続指向ミニポートドライバーでは、次の統計 Oid の64ビットカウンターがサポートされている必要があります。 さらに、次の統計 Oid の64ビットカウンターをサポートすることをお勧めします。

[OID_GEN_CO_XMIT_PDUS_OK](oid-gen-co-xmit-pdus-ok.md)

[OID_GEN_CO_RCV_PDUS_OK](oid-gen-co-rcv-pdus-ok.md)

[OID_GEN_CO_BYTES_XMIT](oid-gen-co-bytes-xmit.md)

[OID_GEN_CO_BYTES_RCV](oid-gen-co-bytes-rcv.md)

このようなミニポートドライバーでは、送信または受信エラーを示す Oid など、他の統計 Oid の64ビットカウンターもサポートできます。

64ビットカウンターのシステムサポートは、Windows XP 以降のバージョンで使用できます。


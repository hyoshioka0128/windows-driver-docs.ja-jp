---
title: NDIS 一般統計情報 OID
description: このセクションには、すべての NDIS ドライバーの全般的な統計の Oid がについて説明します
keywords:
- NDIS 一般統計情報 OID
- WDK NDIS 全般的な統計の Oid
- WDK の全般的な統計の Oid
ms.assetid: 364BEF6E-489C-427A-9ACC-D18F29F22B0F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5db4f4d8b24819adb10db7e8537f41db9e6e9a94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385517"
---
# <a name="ndis-general-statistics-oids"></a>NDIS 一般統計情報 OID

ドライバーは、セキュリティの問題への対応が、ドライバーは、オペレーティング システムとアプリケーション ネットワークの状態を監視するために必要な情報を提供できるように完全な情報と OID 統計情報のクエリに応答して、問題を診断する必要があります。 統計カウンターがハードウェアである場合は、ドライバー統計情報の適切な値から読み取らハードウェア OID の統計情報のクエリを実行するたびにします。

## <a name="miniport-driver-support-for-64-bit-counters"></a>64 ビットのカウンターのミニポート ドライバーのサポート

すべての 1 Gbps、高速のミニポート ドライバーは、以下の統計情報の Oid の 64 ビットのカウンターをサポートする必要があります。 さらに、Microsoft では、100 mbps と高速のミニポート ドライバーをすべてが以下の統計情報の Oid の 64 ビットのカウンターをサポートをお勧めします。

- [OID_GEN_STATISTICS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)
- [OID_GEN_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-rcv)
- [OID_GEN_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-xmit)
- [OID_GEN_RCV_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-discards)
- [OID_GEN_XMIT_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-discards)
- [OID_GEN_XMIT_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok)
- [OID_GEN_RCV_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok)
- [OID_GEN_XMIT_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error)
- [OID_GEN_RCV_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error)
- [OID_GEN_RCV_NO_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-no-buffer)
- [OID_GEN_DIRECTED_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit)
- [OID_GEN_DIRECTED_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit)
- [OID_GEN_MULTICAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit)
- [OID_GEN_MULTICAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit)
- [OID_GEN_BROADCAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit)
- [OID_GEN_BROADCAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit)
- [OID_GEN_DIRECTED_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv)
- [OID_GEN_DIRECTED_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv)
- [OID_GEN_MULTICAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv)
- [OID_GEN_MULTICAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv)
- [OID_GEN_BROADCAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv)
- [OID_GEN_BROADCAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv)
- [OID_GEN_RCV_CRC_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-crc-error)
- [OID_GEN_TRANSMIT_QUEUE_LENGTH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-queue-length)
- [OID_GEN_INIT_TIME_MS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-init-time-ms)
- [OID_GEN_RESET_COUNTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-reset-counts)
- [OID_GEN_MEDIA_SENSE_COUNTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-sense-counts)

ミニポート ドライバーでは、他の統計情報の送信を示すまたはエラーを受信する Oid などの Oid の 64 ビットのカウンターもサポートできます。

64 ビットのカウンターのシステムのサポートは Windows XP およびそれ以降のオペレーティング システムで使用できます。

>[!NOTE]
> NDIS MUX driver miniport の複数のインスタンスを公開する場合、次の全般的な統計の Oid のクエリを実行する必要がありますにデータを返す特定ミニポート インスタンスを。 たとえば、MUX driver は、仮想ローカル エリア ネットワーク (VLAN) のフィルター処理を実装し、1 つの VLAN の 1 つのミニポートの公開する場合、VLAN ごとに次の Oid から返される統計値が必要です。
> - [OID_GEN_STATISTICS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)
> - [OID_GEN_RCV_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok)
> - [OID_GEN_XMIT_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok)



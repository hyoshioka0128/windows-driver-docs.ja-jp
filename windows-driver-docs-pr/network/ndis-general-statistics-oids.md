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
ms.openlocfilehash: 2a6b69fb0666debcc5a2b7700e3483970e7b3309
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392917"
---
# <a name="ndis-general-statistics-oids"></a>NDIS 一般統計情報 OID

ドライバーは、セキュリティの問題への対応が、ドライバーは、オペレーティング システムとアプリケーション ネットワークの状態を監視するために必要な情報を提供できるように完全な情報と OID 統計情報のクエリに応答して、問題を診断する必要があります。 統計カウンターがハードウェアである場合は、ドライバー統計情報の適切な値から読み取らハードウェア OID の統計情報のクエリを実行するたびにします。

## <a name="miniport-driver-support-for-64-bit-counters"></a>64 ビットのカウンターのミニポート ドライバーのサポート

すべての 1 Gbps、高速のミニポート ドライバーは、以下の統計情報の Oid の 64 ビットのカウンターをサポートする必要があります。 さらに、Microsoft では、100 mbps と高速のミニポート ドライバーをすべてが以下の統計情報の Oid の 64 ビットのカウンターをサポートをお勧めします。

- [OID_GEN_STATISTICS](https://msdn.microsoft.com/library/windows/hardware/ff569640)
- [OID_GEN_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569443)
- [OID_GEN_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569445)
- [OID_GEN_RCV_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569628)
- [OID_GEN_XMIT_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569653)
- [OID_GEN_XMIT_OK](https://msdn.microsoft.com/library/windows/hardware/ff569656)
- [OID_GEN_RCV_OK](https://msdn.microsoft.com/library/windows/hardware/ff569632)
- [OID_GEN_XMIT_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569654)
- [OID_GEN_RCV_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569629)
- [OID_GEN_RCV_NO_BUFFER](https://msdn.microsoft.com/library/windows/hardware/ff569631)
- [OID_GEN_DIRECTED_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569578)
- [OID_GEN_DIRECTED_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569580)
- [OID_GEN_MULTICAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569612)
- [OID_GEN_MULTICAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569614)
- [OID_GEN_BROADCAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569440)
- [OID_GEN_BROADCAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569442)
- [OID_GEN_DIRECTED_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569577)
- [OID_GEN_DIRECTED_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569579)
- [OID_GEN_MULTICAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569611)
- [OID_GEN_MULTICAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569613)
- [OID_GEN_BROADCAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569439)
- [OID_GEN_BROADCAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569441)
- [OID_GEN_RCV_CRC_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569627)
- [OID_GEN_TRANSMIT_QUEUE_LENGTH](https://msdn.microsoft.com/library/windows/hardware/ff569646)
- [OID_GEN_INIT_TIME_MS](https://msdn.microsoft.com/library/windows/hardware/ff569588)
- [OID_GEN_RESET_COUNTS](https://msdn.microsoft.com/library/windows/hardware/ff569638)
- [OID_GEN_MEDIA_SENSE_COUNTS](https://msdn.microsoft.com/library/windows/hardware/ff569608)

ミニポート ドライバーでは、他の統計情報の送信を示すまたはエラーを受信する Oid などの Oid の 64 ビットのカウンターもサポートできます。

64 ビットのカウンターのシステムのサポートは Windows XP およびそれ以降のオペレーティング システムで使用できます。

>[!NOTE]
> NDIS MUX driver miniport の複数のインスタンスを公開する場合、次の全般的な統計の Oid のクエリを実行する必要がありますにデータを返す特定ミニポート インスタンスを。 たとえば、MUX driver は、仮想ローカル エリア ネットワーク (VLAN) のフィルター処理を実装し、1 つの VLAN の 1 つのミニポートの公開する場合、VLAN ごとに次の Oid から返される統計値が必要です。
> - [OID_GEN_STATISTICS](https://msdn.microsoft.com/library/windows/hardware/ff569640)
> - [OID_GEN_RCV_OK](https://msdn.microsoft.com/library/windows/hardware/ff569632)
> - [OID_GEN_XMIT_OK](https://msdn.microsoft.com/library/windows/hardware/ff569656)



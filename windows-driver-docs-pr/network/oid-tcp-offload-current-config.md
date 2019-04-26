---
title: OID_TCP_OFFLOAD_CURRENT_CONFIG
description: このトピックでは、OID_TCP_OFFLOAD_CURRENT_CONFIG オブジェクト識別子 (OID) について説明します。
ms.assetid: 8DC81A41-1E4D-4F78-80D1-54C79F974CE3
keywords:
- OID_TCP_OFFLOAD_CURRENT_CONFIG、WDK の Oid、WDK のオブジェクト識別子では、WDK の Oid をネットワークのネットワーク
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7472dc34fec0c8c2f14e252d6d262efc7d1c36e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354155"
---
# <a name="oidtcpoffloadcurrentconfig"></a>OID_TCP_OFFLOAD_CURRENT_CONFIG

クエリの要求としての管理アプリケーション (またはドライバーの上にある可能性があります) は、基になるミニポート アダプターの現在タスク オフロードの構成設定を確認するのに OID_TCP_OFFLOAD_CURRENT_CONFIG OID を使用します。 システム管理者は、この OID を使用して、Microsoft Windows Management Instrumentation (WMI) インターフェイスを使用できます。

要求のセットがサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、ミニポート ドライバーには、この OID を処理します。 ミニポート ドライバーでは、NDIS ミニポート アダプター オフロード機能を報告します。 渡すタスクに関する情報の構成設定にオフロード NDIS ミニポート ドライバーおよび NDIS からドライバーに関連する NDIS_OFFLOAD を参照してください。

**InformationBuffer**のメンバー、 [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [NDIS_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff566599)構造体。 **NDIS_OFFLOAD**構造には、次のミニポート アダプターの機能が含まれます。

- ヘッダーは、タスクのオフロード バージョンが含まれています。
- チェックサムでは、負荷を軽減する[NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567878)構造体。
- 大規模なオフロード バージョン 1 (LSOV1) を送信する情報で、 [NDIS_TCP_LARGE_SEND_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff567883)構造体。
- インターネット プロトコル セキュリティ (IPsec) については、ので、 [NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)構造体。
- 大規模なオフロード バージョン 2 (LSOV2) を送信する情報で、 [NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://msdn.microsoft.com/library/windows/hardware/ff567884)構造体。

OID_TCP_OFFLOAD_CURRENT_CONFIG への応答、**カプセル化**上記の構造体のメンバーがミニポート アダプタのパケット カプセル化機能を定義します。 NDIS に用意されているフラグのビットごとの OR の提供、**カプセル化**これらの構造体のメンバー。 その他の構造体のメンバーには、さまざまなオフロード サービスの設定が含まれます。 カプセル化およびその他の機能の詳細については、次を参照してください[NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567878)、 [NDIS_TCP_LARGE_SEND_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff567883)、 [NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)。、および[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://msdn.microsoft.com/library/windows/hardware/ff567884)します。

ミニポート アダプターでは、カプセル化タスクの種類のすべてのオフロードをサポートしているイーサネットをサポートする必要があります。 他の種類のカプセル化は省略可能です。

初期化中にすべてのタスクのオフロード機能ミニポート ドライバーに有効自動的にする必要があります。

### <a name="see-also"></a>関連項目

[NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)  
[NDIS_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff566599)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567878)  
[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://msdn.microsoft.com/library/windows/hardware/ff567884)    
[NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)  

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


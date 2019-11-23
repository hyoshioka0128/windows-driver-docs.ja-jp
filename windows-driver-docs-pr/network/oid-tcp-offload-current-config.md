---
title: OID_TCP_OFFLOAD_CURRENT_CONFIG
description: このトピックでは、OID_TCP_OFFLOAD_CURRENT_CONFIG オブジェクト識別子 (OID) について説明します。
ms.assetid: 8DC81A41-1E4D-4F78-80D1-54C79F974CE3
keywords:
- OID_TCP_OFFLOAD_CURRENT_CONFIG、wdk Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5db248e281e0c51b0760e60169d6344df4dfb14
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843905"
---
# <a name="oid_tcp_offload_current_config"></a>OID_TCP_OFFLOAD_CURRENT_CONFIG

クエリ要求として、管理アプリケーション (またはそれ以降のドライバー) は、基になるミニポートアダプターの現在のタスクオフロード構成設定を判断するために OID_TCP_OFFLOAD_CURRENT_CONFIG OID を使用します。 システム管理者は、この OID を Microsoft Windows Management Instrumentation (WMI) インターフェイスで使用できます。

Set 要求はサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、この OID をミニポートドライバー用に処理します。 ミニポートドライバーは、ミニポートアダプターのオフロード機能を NDIS に報告します。 ミニポートドライバーから NDIS にタスクオフロード構成設定を渡す方法と、NDIS からそれ以降のドライバーに渡す方法については、「NDIS_OFFLOAD」を参照してください。

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体が含まれています。 **NDIS_OFFLOAD**構造には、次のミニポートアダプターの機能が含まれています。

- タスクオフロードバージョンを含むヘッダー情報。
- [NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)構造内のチェックサムオフロード情報。
- [NDIS_TCP_LARGE_SEND_OFFLOAD_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)構造での large send offload version 1 (LSOV1) の情報。
- [NDIS_IPSEC_OFFLOAD_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)構造体のインターネットプロトコルセキュリティ (IPsec) 情報。
- [NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)構造での large send offload version 2 (LSOV2) の情報。

OID_TCP_OFFLOAD_CURRENT_CONFIG に応答して、前の一覧の構造体の**カプセル化**メンバーは、ミニポートアダプターのパケットカプセル化機能を定義します。 NDIS は、これらの構造体の**カプセル化**メンバーに用意されているフラグのビットごとの or を提供します。 他の構造体のメンバーには、さまざまなオフロードサービスの設定が含まれています。 カプセル化とその他の機能の詳細については、「 [NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)、 [NDIS_TCP_LARGE_SEND_OFFLOAD_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)、 [NDIS_IPSEC_OFFLOAD_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)、および[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)」を参照してください。

ミニポートアダプターは、サポートするすべての種類のタスクオフロードに対してイーサネットカプセル化をサポートする必要があります。 その他の種類のカプセル化はオプションです。

ミニポートドライバーは、初期化中にすべてのタスクオフロード機能を自動的に有効にする必要があります。

### <a name="see-also"></a>関連項目

[NDIS_IPSEC_OFFLOAD_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)  
[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)  
[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)    
[NDIS_IPSEC_OFFLOAD_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)  

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |


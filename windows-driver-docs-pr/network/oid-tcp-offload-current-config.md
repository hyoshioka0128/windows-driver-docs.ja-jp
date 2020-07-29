---
title: OID_TCP_OFFLOAD_CURRENT_CONFIG
description: このトピックでは、OID_TCP_OFFLOAD_CURRENT_CONFIG オブジェクト識別子 (OID) について説明します。
ms.assetid: 8DC81A41-1E4D-4F78-80D1-54C79F974CE3
keywords:
- OID_TCP_OFFLOAD_CURRENT_CONFIG、wdk Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 02/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: e02308cedd70ce7dac411536a8f1d147cac32914
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264443"
---
# <a name="oid_tcp_offload_current_config"></a>OID_TCP_OFFLOAD_CURRENT_CONFIG

クエリ要求として、管理アプリケーション (またはそれ以降のドライバー) は、基になるミニポートアダプターの現在のタスクオフロード構成設定を判断するために OID_TCP_OFFLOAD_CURRENT_CONFIG OID を使用します。 システム管理者は、この OID を Microsoft Windows Management Instrumentation (WMI) インターフェイスで使用できます。

Set 要求はサポートされていません。

## <a name="remarks"></a>解説

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

## <a name="requirements"></a>必要条件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

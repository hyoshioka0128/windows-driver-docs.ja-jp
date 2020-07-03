---
title: OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG オブジェクト識別子 (OID) について説明します。
ms.assetid: 29CB74B1-8D7F-4EC2-AAAC-93D454824031
keywords:
- OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG、wdk Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936fa26b6e6caeb49d93b5089cfc34d10d5a1155
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917646"
---
# <a name="oid_tcp_connection_offload_current_config"></a>OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG

クエリ要求として、管理アプリケーション (またはそれ以降のドライバー) は、OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG OID を使用して、基になるミニポートアダプターの現在有効な接続オフロード機能を判断できます。 システム管理者は、この OID を Microsoft Windows Management Instrumentation (WMI) インターフェイスで使用できます。

Set 要求はサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、この OID をミニポートドライバー用に処理します。 ミニポートドライバーは、ミニポートアダプターの接続オフロード設定を NDIS に報告します。 ミニポートドライバーから NDIS に接続のオフロード構成設定を渡す方法と、NDIS からそれ以降のドライバーに渡す方法については、「 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)」を参照してください。

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造体が含まれています。

OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG に応答して、NDIS_TCP_CONNECTION_OFFLOAD の**カプセル化**メンバーは、ミニポートアダプターの現在のパケットカプセル化構成を定義します。 NDIS は、**カプセル化**メンバーに用意されているフラグのビットごとの or を提供します。 NDIS_TCP_CONNECTION_OFFLOAD の他のメンバーには、さまざまな接続オフロードサービスの設定が含まれています。 カプセル化とその他の機能の詳細については、「 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) 」および「 [NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)」を参照してください。


### <a name="see-also"></a>こちらもご覧ください

[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)


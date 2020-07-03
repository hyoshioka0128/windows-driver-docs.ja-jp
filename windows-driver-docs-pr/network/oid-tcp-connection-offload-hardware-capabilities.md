---
title: OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES オブジェクト識別子 (OID) について説明します。
ms.assetid: E90EC9E5-4667-4CBF-8812-06FB45331368
keywords:
- OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES、wdk Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c27eec05a4aa22749c836d58595c41e1f13628e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916151"
---
# <a name="oid_tcp_connection_offload_hardware_capabilities"></a>OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES

クエリ要求として、OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES OID は、基になるミニポートアダプターの現在の接続オフロードハードウェア機能を報告します。 ユーザーモードアプリケーション (またはそれ以降のドライバー) は、この OID に対してクエリを実行し、基になるミニポートアダプターの接続オフロードハードウェア機能を決定することができます。 システム管理者は、この OID を Microsoft Windows Management Instrumentation (WMI) インターフェイスで使用できます。

Set 要求はサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、この OID をミニポートドライバー用に処理します。 ミニポートドライバーは、ミニポートアダプター接続オフロードハードウェア機能を NDIS に報告します。 ミニポートドライバーから NDIS に接続オフロードハードウェア機能を渡す方法と、NDIS からそれ以降のドライバーに渡す方法については、「 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)」を参照してください。

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造体が含まれています。

OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES に応答して、NDIS_TCP_CONNECTION_OFFLOAD の**カプセル化**メンバーは、ミニポートアダプターの現在のパケットカプセル化ハードウェア機能を定義します。 NDIS は、**カプセル化**メンバーに用意されているフラグのビットごとの or を提供します。 NDIS_TCP_CONNECTION_OFFLOAD の他のメンバーには、さまざまな接続オフロードサービスの設定が含まれています。 カプセル化とその他の機能の詳細については、「 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) 」および「 [NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)」を参照してください。


### <a name="see-also"></a>こちらもご覧ください

[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)


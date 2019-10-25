---
title: OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES オブジェクト識別子 (OID) について説明します。
ms.assetid: E90EC9E5-4667-4CBF-8812-06FB45331368
keywords:
- OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES、WDK Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ceddf0dbc5153583213be493e3657ff5fdb368
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843909"
---
# <a name="oid_tcp_connection_offload_hardware_capabilities"></a>OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES

クエリ要求として、OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES OID は、基になるミニポートアダプターの現在の接続オフロードハードウェア機能を報告します。 ユーザーモードアプリケーション (またはそれ以降のドライバー) は、この OID に対してクエリを実行し、基になるミニポートアダプターの接続オフロードハードウェア機能を決定することができます。 システム管理者は、この OID を Microsoft Windows Management Instrumentation (WMI) インターフェイスで使用できます。

Set 要求はサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、この OID をミニポートドライバー用に処理します。 ミニポートドライバーは、ミニポートアダプター接続オフロードハードウェア機能を NDIS に報告します。 接続のオフロードハードウェア機能をミニポートドライバーから NDIS に渡す方法と、NDIS から[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)ドライバーに渡す方法については、「」を参照してください。

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)構造体が含まれています。

OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES への応答として、NDIS_TCP_CONNECTION_OFFLOAD の**カプセル化**メンバーは、ミニポートアダプターの現在のパケットカプセル化ハードウェア機能を定義します。 NDIS は、**カプセル化**メンバーに用意されているフラグのビットごとの or を提供します。 NDIS_TCP_CONNECTION_OFFLOAD の他のメンバーには、さまざまな接続オフロードサービスの設定が含まれています。 カプセル化とその他の機能の詳細については、「 [NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) and [NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)」を参照してください。


### <a name="see-also"></a>関連項目

[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |


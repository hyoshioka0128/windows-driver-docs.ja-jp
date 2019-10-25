---
title: OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES
description: このトピックでは、OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES オブジェクト識別子 (OID) について説明します。
ms.assetid: 9958F93C-0D68-428B-A25C-7FF6E4F37702
keywords:
- OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES、WDK Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3556bce13adf5ec9bb5a587cc5082c0b3afc6ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843903"
---
# <a name="oid_tcp_offload_hardware_capabilities"></a>OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES

OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES OID は、クエリ要求として、ミニポートアダプターのハードウェアのタスクオフロードハードウェア機能を報告します。 ユーザーモードアプリケーション (またはそれ以降のドライバー) は、この OID に対してクエリを実行し、基になるミニポートアダプターのタスクオフロードハードウェア機能を決定することができます。 システム管理者は、Windows Management Instrumentation (WMI) インターフェイスを使用して、この OID を使用できます。

Set 要求はサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、この OID をミニポートドライバー用に処理します。 ミニポートドライバーは、ミニポートアダプターのハードウェア機能を NDIS に報告します。 ミニポートドライバーから NDIS へのレポートタスクオフロードハードウェア機能と、NDIS からそれ以降のドライバーについては、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)を参照してください。

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体が含まれています。 バッファーの大きさが十分でない場合、NDIS は NDIS_STATUS_BUFFER_TOO_SHORT を返します。

ミニポートアダプターのハードウェア機能を決定した後、 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID を使用して、OID_TCP_OFFLOAD_CURRENT によって無効として現在報告されている機能を有効にすることができます。 [構成 OID (_C)](oid-tcp-offload-current-config.md)

### <a name="see-also"></a>関連項目

[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)  

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |


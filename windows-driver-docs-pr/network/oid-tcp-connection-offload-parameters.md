---
title: OID_TCP_CONNECTION_OFFLOAD_PARAMETERS
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS オブジェクト識別子 (OID) について説明します。
ms.assetid: 6481D565-900A-4B75-A60F-72701FB45FAD
keywords:
- OID_TCP_CONNECTION_OFFLOAD_PARAMETERS、wdk Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3d4a1b229dfb4be81bdb4854255b82950cc6926
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916801"
---
# <a name="oid_tcp_connection_offload_parameters"></a>OID_TCP_CONNECTION_OFFLOAD_PARAMETERS

クエリ要求として、後続のドライバーは OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID を使用して、基になるミニポートアダプターの現在の接続オフロード設定を判断できます。 NDIS は、この OID クエリをミニポートドライバーに対して処理します。

NDIS およびそれ以降のドライバーは、セット要求として、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID を使用して、基になるミニポートアダプターの接続オフロード構成パラメーターを設定します。 接続オフロードをサポートするミニポートドライバーは、この OID セット要求を処理する必要があります。 それ以外の場合、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID はミニポートドライバーでは省略可能です。

## <a name="remarks"></a>注釈

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_TCP_CONNECTION_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_tcp_connection_offload_parameters)構造体が含まれています。

> [!NOTE]
> OID_TCP_CONNECTION_OFFLOAD_PARAMETERS は、管理アプリケーションが TCP オフロード機能を有効または無効にするために使用する[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID と混同しないようにしてください。

### <a name="see-also"></a>こちらもご覧ください

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)


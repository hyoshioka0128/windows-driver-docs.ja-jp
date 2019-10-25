---
title: OID_TCP_CONNECTION_OFFLOAD_PARAMETERS
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS オブジェクト識別子 (OID) について説明します。
ms.assetid: 6481D565-900A-4B75-A60F-72701FB45FAD
keywords:
- OID_TCP_CONNECTION_OFFLOAD_PARAMETERS、WDK Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: a30f17bf5e126bc464d5b53a7d73a23ee15d834a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843908"
---
# <a name="oid_tcp_connection_offload_parameters"></a>OID_TCP_CONNECTION_OFFLOAD_PARAMETERS

クエリ要求として、後続のドライバーは OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID を使用して、基になるミニポートアダプターの現在の接続オフロード設定を判断できます。 NDIS は、この OID クエリをミニポートドライバーに対して処理します。

NDIS およびそれ以降のドライバーは、set 要求として、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID を使用して、基になるミニポートアダプターの接続オフロード構成パラメーターを設定します。 接続オフロードをサポートするミニポートドライバーは、この OID セット要求を処理する必要があります。 それ以外の場合、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID はミニポートドライバーでは省略可能です。

## <a name="remarks"></a>注釈

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_TCP_CONNECTION_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_tcp_connection_offload_parameters)構造体が含まれています。

> [!NOTE]
> OID_TCP_CONNECTION_OFFLOAD_PARAMETERS は、管理アプリケーションが TCP オフロード機能を有効または無効にするために使用する[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID と混同しないようにしてください。

### <a name="see-also"></a>関連項目

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |


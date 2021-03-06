---
title: OID_TCP_CONNECTION_OFFLOAD_PARAMETERS
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS オブジェクト識別子 (OID) について説明します。
ms.assetid: 6481D565-900A-4B75-A60F-72701FB45FAD
keywords:
- OID_TCP_CONNECTION_OFFLOAD_PARAMETERS、WDK の Oid、WDK のオブジェクト識別子では、WDK の Oid をネットワークのネットワーク
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb8b498dd5c62883d7dae05056d353416941712
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386967"
---
# <a name="oidtcpconnectionoffloadparameters"></a>OID_TCP_CONNECTION_OFFLOAD_PARAMETERS

クエリの要求としてドライバーに関連を使用できます OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID、基になるミニポート アダプターの現在の接続のオフロード設定を確認します。 NDIS は、ミニポート ドライバーには、この OID クエリを処理します。

セットの要求としての接続を設定する NDIS と重なって OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID のドライバーが使用は、基になるミニポート アダプターの構成パラメーターをオフロードします。 接続のオフロードをサポートするミニポート ドライバーには、この OID のセット要求を処理する必要があります。 それ以外の場合、OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID は、ミニポート ドライバーにもあります。

## <a name="remarks"></a>注釈

**InformationBuffer**のメンバー、 [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に含まれる、 [NDIS_TCP_CONNECTION_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_tcp_connection_offload_parameters)構造体。

> [!NOTE]
> OID_TCP_CONNECTION_OFFLOAD_PARAMETERS とを混同しないでください、 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)オフロード機能を有効または TCP を無効にする管理アプリケーションで使用される OID。

### <a name="see-also"></a>関連項目

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


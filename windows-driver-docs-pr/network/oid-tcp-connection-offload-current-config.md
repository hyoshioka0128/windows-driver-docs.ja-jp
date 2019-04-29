---
title: OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG オブジェクト識別子 (OID) について説明します。
ms.assetid: 29CB74B1-8D7F-4EC2-AAAC-93D454824031
keywords:
- OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG、WDK の Oid、WDK のオブジェクト識別子では、WDK の Oid をネットワークのネットワーク
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a02d0bde9107284dccdec13092bdf818840a74c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331811"
---
# <a name="oidtcpconnectionoffloadcurrentconfig"></a>OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG

クエリの要求としての管理アプリケーション (またはドライバーの上にある可能性があります) は、基になるミニポート アダプターの現在の有効な接続のオフロード機能を決定するのに OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG OID を使用できます。 システム管理者は、この OID を使用して、Microsoft Windows Management Instrumentation (WMI) インターフェイスを使用できます。

要求のセットがサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、ミニポート ドライバーには、この OID を処理します。 ミニポート ドライバーに NDIS ミニポート アダプター接続オフロード設定を報告します。 接続オフロードの構成に設定を渡す NDIS ミニポート ドライバーおよび NDIS から上にあるドライバーについては、次を参照してください。 [NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)します。

**InformationBuffer**のメンバー、 [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)構造体。

OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG への応答、**カプセル化**NDIS_TCP_CONNECTION_OFFLOAD のメンバーがミニポート アダプターの現在のパケット カプセル化の構成を定義します。 NDIS に用意されているフラグのビットごとの OR の提供、**カプセル化**メンバー。 NDIS_TCP_CONNECTION_OFFLOAD の他のメンバーには、さまざまな接続のオフロード サービスの設定が含まれます。 カプセル化およびその他の機能の詳細については、次を参照してください。 [NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)と[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)します。


### <a name="see-also"></a>関連項目

[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


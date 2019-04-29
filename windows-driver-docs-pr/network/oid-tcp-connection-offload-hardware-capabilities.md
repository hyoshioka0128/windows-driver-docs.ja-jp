---
title: OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: このトピックでは、OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES オブジェクト識別子 (OID) について説明します。
ms.assetid: E90EC9E5-4667-4CBF-8812-06FB45331368
keywords:
- OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES、WDK の Oid、WDK のオブジェクト識別子では、WDK の Oid をネットワークのネットワーク
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: b30f73ac9405a5063d3166bca76bbf9f7823845c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331825"
---
# <a name="oidtcpconnectionoffloadhardwarecapabilities"></a>OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES

クエリの要求として OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES OID は、基になるミニポート アダプターの現在の接続オフロード ハードウェアの機能を報告します。 ユーザー モード アプリケーション (またはドライバーの上にある可能性があります) は、基になるミニポート アダプターの接続のオフロード ハードウェア機能を決定するには、この OID を照会できます。 システム管理者は、この OID を使用して、Microsoft Windows Management Instrumentation (WMI) インターフェイスを使用できます。

要求のセットがサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、ミニポート ドライバーには、この OID を処理します。 ミニポート ドライバーはレポートには、NDIS ミニポート アダプター接続オフロード ハードウェア機能です。 接続オフロード ハードウェア機能に渡す NDIS ミニポート ドライバーおよび NDIS から上にあるドライバーについては、次を参照してください。 [NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)します。

**InformationBuffer**のメンバー、 [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)構造体。

OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES への応答、**カプセル化**NDIS_TCP_CONNECTION_OFFLOAD のメンバーがミニポート アダプターの現在のパケット カプセル化ハードウェアの機能を定義します。 NDIS に用意されているフラグのビットごとの OR の提供、**カプセル化**メンバー。 NDIS_TCP_CONNECTION_OFFLOAD の他のメンバーには、さまざまな接続のオフロード サービスの設定が含まれます。 カプセル化およびその他の機能の詳細については、次を参照してください。 [NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)と[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)します。


### <a name="see-also"></a>関連項目

[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


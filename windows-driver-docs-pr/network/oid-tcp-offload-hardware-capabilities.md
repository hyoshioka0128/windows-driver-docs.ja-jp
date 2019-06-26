---
title: OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES
description: このトピックでは、OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES オブジェクト識別子 (OID) について説明します。
ms.assetid: 9958F93C-0D68-428B-A25C-7FF6E4F37702
keywords:
- OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES、WDK の Oid、WDK のオブジェクト識別子では、WDK の Oid をネットワークのネットワーク
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ba72d60d8adc52b40dc97e2a752cd99535a8710
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386962"
---
# <a name="oidtcpoffloadhardwarecapabilities"></a>OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES

クエリの要求として OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES OID はミニポート アダプターのハードウェアのタスクのオフロード ハードウェア機能を報告します。 ユーザー モード アプリケーション (またはドライバーの上にある可能性があります) は、基になるミニポート アダプターのタスクのオフロード ハードウェア機能を決定するには、この OID を照会できます。 システム管理者は、この OID を使用して、Windows Management Instrumentation (WMI) インターフェイスを使用できます。

要求のセットがサポートされていません。

## <a name="remarks"></a>注釈

NDIS は、ミニポート ドライバーには、この OID を処理します。 ミニポート ドライバーでは、NDIS ミニポート アダプター ハードウェア機能を報告します。 レポート タスク オフロードのハードウェア機能を NDIS ミニポート ドライバーおよび NDIS から上にあるドライバーについては、次を参照してください。 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)します。

**InformationBuffer**のメンバー、 [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に含まれる、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。 NDIS は、バッファーの大きさがない場合、NDIS_STATUS_BUFFER_TOO_SHORT を返します。

上位のアプリケーションまたはドライバーを使用できます、ミニポート アダプターのハードウェア機能を決定した後、 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) によって報告される現在の機能を有効にするOIDが有効にしないように[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md) OID。

### <a name="see-also"></a>関連項目

[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)  

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


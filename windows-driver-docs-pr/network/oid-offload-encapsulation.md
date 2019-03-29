---
title: OID_OFFLOAD_ENCAPSULATION
description: このトピックでは、OID_OFFLOAD_ENCAPSULATION オブジェクト識別子 (OID) について説明します。
ms.assetid: 8B5BE43C-1004-427A-B16D-5A2AA34C96CD
keywords:
- OID_OFFLOAD_ENCAPSULATION、WDK の Oid、WDK のオブジェクト識別子では、WDK の Oid をネットワークのネットワーク
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fd894fa568a50c77207243c2f1c59e8c88d7027
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571398"
---
# <a name="oidoffloadencapsulation"></a>OID_OFFLOAD_ENCAPSULATION

クエリの要求としては、上にあるドライバーは、基になるミニポート アダプターのオフロード カプセル化の設定を取得するには、現在のタスクを OID_OFFLOAD_ENCAPSULATION OID を使用します。 NDIS は、ミニポート ドライバーには、この OID クエリを処理します。

セットの要求としては、上にあるドライバーは、タスクの基になるミニポート アダプターのオフロード カプセル化の設定を設定するのに OID_OFFLOAD_ENCAPSULATION OID を使用します。 タスク オフロードをサポートするミニポート ドライバーでは、この OID セット要求を処理する必要があります。

## <a name="remarks"></a>コメント

InformationBuffer メンバー、 [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [NDIS_OFFLOAD_ENCAPSULATION](https://msdn.microsoft.com/library/windows/hardware/ff566702)構造体。

### <a name="miniport-drivers"></a>ミニポート ドライバー

ミニポート ドライバーは、オフロードとこの OID をサポートしていない、ドライバーは NDIS_STATUS_NOT_SUPPORTED を返す必要があります。

ミニポート ドライバーの内容を使用する必要があります、 [NDIS_OFFLOAD_ENCAPSULATION](https://msdn.microsoft.com/library/windows/hardware/ff566702)オフロード機能の報告される現在の TCP を更新する構造体。 ミニポート ドライバーの更新後では、現在のタスク オフロード機能を報告する必要があります、 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状態を示す値。 この状態を示す値により、新しい機能の情報ですべての上位のプロトコルのドライバーが更新されるようになります。

この OID を使用してすべての構成済みまたは有効なオフロードをアクティブ化またはすべてのオフロードを非アクティブ化 (つまり、ハードウェア開始する、オフロードを実行する)。 個々 のオフロードを細かく制御は提供されません。 代わりに、 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)は個々 のオフロードを構成に使用されできますもそれらをアクティブ化します。 一般に、ほとんどの TCP/IP タスク オフロードを構成および OID_TCP_OFFLOAD_PARAMETERS でアクティブ化します。

ただし、この OID の NDIS_OFFLOAD_ENCAPSULATION 構造についても説明します OID_TCP_OFFLOAD_PARAMETERS のカバーされないその他の 2 つのカプセル化型[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)構造体。**NDIS_ENCAPSULATION_IEEE_802_3**と**NDIS_ENCAPSULATION_IEEE_LLC_SNAP_ROUTED**します。 ミニポート ドライバーでは、さまざまな Oid でカバーされるカプセル化の種類の違いを処理する必要があります。

この OID はすべてオフロードは、非アクティブ化するプロトコル ドライバーによって発行されている場合、**有効**NDIS_OFFLOAD_ENCAPSULATION メンバーのメンバーは NDIS_OFFLOAD_SET_OFF に設定されます。

### <a name="setting-encapsulation-protocol-drivers"></a>設定のカプセル化 (プロトコル ドライバー)

プロトコル ドライバーは、カプセル化のシステム要件を決定した後、OID_OFFLOAD_ENCAPSULATION を設定します。 プロトコル ドライバーは、基になるミニポート アダプターからの機能を決定できます、 [NDIS_BIND_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体またはでクエリを実行する[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)します。 プロトコル ドライバーには、ミニポート アダプターが少なくとも 1 つのオフロード サービスをサポートする、カプセル化の種類を設定する必要があります。

ミニポート ドライバーでは、要求されたカプセル化の種類をサポートする任意のオフロード型をサポートする場合、ドライバーは OID_OFFLOAD_ENCAPSULATION のセットへの応答で NDIS_STATUS_SUCCESS を返す必要があります。 それ以外の場合、ミニポート ドライバーでは、NDIS_STATUS_INVALID_PARAMETER を返す必要があります。

送信操作では、プロトコル ドライバーは、ミニポート アダプターが必要なカプセル化の種類をサポートするオフロード型のみを使用して送信要求を発行できます。 そのため、OID の OID_OFFLOAD_ENCAPSULATION が失敗した要求を設定する場合プロトコル ドライバーで使用しないでくださいオフロード設定そのミニポート アダプターに送信される要求を送信します。

受信操作、ミニポート ドライバーは、チェックサムを開始する必要がありますか、OID OID_OFFLOAD_ENCAPSULATION の要求の設定を受信した後になるまで、インターネット プロトコル セキュリティ (IPsec) オフロード サービス。

### <a name="obtaining-current-encapsulation-settings-protocol-drivers"></a>現在のカプセル化の設定 (プロトコル ドライバー) を取得します。

プロトコル ドライバーには、OID_OFFLOAD_ENCAPSULATION OID を設定した後にのみ、OID_OFFLOAD_ENCAPSULATION クエリを発行できます。

NDIS はで応答を[NDIS_OFFLOAD_ENCAPSULATION](https://msdn.microsoft.com/library/windows/hardware/ff566702)カプセル化の現在の設定を含む構造体。

プロトコル ドライバーは、NDIS_STATUS_Xxx エラー コードを処理するために準備する必要があります。 プロトコル ドライバーにエラーが発生した場合、影響を受けるミニポート アダプターに転送されるオフロード操作を実行する読み取ろうとしないでします。

### <a name="see-also"></a>関連項目

[NDIS_BIND_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff564832)  
[NDIS_OFFLOAD_ENCAPSULATION](https://msdn.microsoft.com/library/windows/hardware/ff566702)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


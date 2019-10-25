---
title: OID_OFFLOAD_ENCAPSULATION
description: このトピックでは、OID_OFFLOAD_ENCAPSULATION オブジェクト識別子 (OID) について説明します。
ms.assetid: 8B5BE43C-1004-427A-B16D-5A2AA34C96CD
keywords:
- OID_OFFLOAD_ENCAPSULATION、WDK Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fdc59d9d7d23d09ca28573b73170488228add82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844073"
---
# <a name="oid_offload_encapsulation"></a>OID_OFFLOAD_ENCAPSULATION

クエリ要求として、後続のドライバーは OID_OFFLOAD_ENCAPSULATION OID を使用して、基になるミニポートアダプターの現在のタスクオフロードカプセル化設定を取得します。 NDIS は、この OID クエリをミニポートドライバーに対して処理します。

設定要求として、後続のドライバーは OID_OFFLOAD_ENCAPSULATION OID を使用して、基になるミニポートアダプターのタスクオフロードカプセル化設定を設定します。 タスクオフロードをサポートするミニポートドライバーは、この OID セット要求を処理する必要があります。

## <a name="remarks"></a>注釈

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の informationbuffer メンバーには、 [NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)構造体が含まれています。

### <a name="miniport-drivers"></a>ミニポート ドライバー

ミニポートドライバーでオフロードとこの OID がサポートされていない場合、ドライバーは NDIS_STATUS_NOT_SUPPORTED を返す必要があります。

ミニポートドライバーは、 [NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)構造体の内容を使用して、現在報告されている TCP オフロード機能を更新する必要があります。 更新後、ミニポートドライバーは、現在のタスクオフロード機能を[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)ステータスを示す情報と共に報告する必要があります。 この状態の表示により、すべてのプロトコルドライバーが新機能の情報で更新されます。

この OID は、すべての構成済みまたは有効なオフロードのアクティブ化、またはすべてのオフロードを非アクティブ化するために使用されます (つまり、ハードウェアはオフロードの実行を開始します)。 個々のオフロードを細かく制御することはできません。 代わりに、 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)を使用して個々のオフロードを構成し、アクティブ化することもできます。 通常、TCP/IP タスクのオフロードは、OID_TCP_OFFLOAD_PARAMETERS を使用して構成およびアクティブ化することができます。

ただし、この OID の NDIS_OFFLOAD_ENCAPSULATION 構造体では、OID_TCP_OFFLOAD_PARAMETERS's [NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters) Structure: **NDIS_ENCAPSULATION_IEEE_802_3**およびでカバーされていない他の2つのカプセル化型についても説明し**ています。NDIS_ENCAPSULATION_IEEE_LLC_SNAP_ROUTED**。 ミニポートドライバーは、異なる Oid によってカバーされるカプセル化の種類の違いに対処する必要があります。

この OID がプロトコルドライバーによって発行され、すべてのオフロードが非アクティブ化されると、NDIS_OFFLOAD_ENCAPSULATION メンバーの**有効な**メンバーが NDIS_OFFLOAD_SET_OFF に設定されます。

### <a name="setting-encapsulation-protocol-drivers"></a>カプセル化の設定 (プロトコルドライバー)

プロトコルドライバーは、システムカプセル化の要件を決定した後に OID_OFFLOAD_ENCAPSULATION を設定します。 プロトコルドライバーでは、基になるミニポートアダプターの機能を[NDIS_BIND_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体から、または[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)に照会することによって特定できます。 プロトコルドライバーでは、少なくとも1つのオフロードサービスでミニポートアダプターがサポートするカプセル化の種類を設定する必要があります。

要求されたカプセル化の種類をサポートするオフロードの種類をミニポートドライバーがサポートしている場合、ドライバーは OID_OFFLOAD_ENCAPSULATION のセットに応答して NDIS_STATUS_SUCCESS を返す必要があります。 それ以外の場合、ミニポートドライバーは NDIS_STATUS_INVALID_PARAMETER を返します。

送信操作の場合、プロトコルドライバーは、ミニポートアダプターが必要なカプセル化の種類でサポートしているオフロードの種類のみを使用して、送信要求を発行できます。 このため、OID_OFFLOAD_ENCAPSULATION の OID セット要求が失敗した場合、そのミニポートアダプターに送られる送信要求では、プロトコルドライバーでオフロード設定を使用できません。

受信操作の場合、ミニポートドライバーは、OID_OFFLOAD_ENCAPSULATION の OID セット要求を受信するまで、チェックサムまたはインターネットプロトコルセキュリティ (IPsec) オフロードサービスを開始することはできません。

### <a name="obtaining-current-encapsulation-settings-protocol-drivers"></a>現在のカプセル化設定の取得 (プロトコルドライバー)

プロトコルドライバーは、OID_OFFLOAD_ENCAPSULATION OID を設定した後にのみ、OID_OFFLOAD_ENCAPSULATION クエリを発行できます。

NDIS は、現在のカプセル化設定を含む[NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)構造体で応答します。

プロトコルドライバーは、NDIS_STATUS_Xxx エラーコードを処理できるように準備する必要があります。 エラーが発生した場合、プロトコルドライバーは、影響を受けるミニポートアダプターに送られるオフロード操作を実行しないようにする必要があります。

### <a name="see-also"></a>関連項目

[NDIS_BIND_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)  
[NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |


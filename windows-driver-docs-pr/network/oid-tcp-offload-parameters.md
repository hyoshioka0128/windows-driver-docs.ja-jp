---
title: OID_TCP_OFFLOAD_PARAMETERS
description: このトピックでは、OID_TCP_OFFLOAD_PARAMETERS オブジェクト識別子 (OID) について説明します。
ms.assetid: 5D9B5F62-E506-4983-B247-A93B81E70A43
keywords:
- OID_TCP_OFFLOAD_PARAMETERS、WDK Oid、WDK ネットワークオブジェクト識別子、WDK ネットワーク Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d3b2d590dcb920d49eb9436fc2e0eaf1cd48f6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843901"
---
# <a name="oid_tcp_offload_parameters"></a>OID_TCP_OFFLOAD_PARAMETERS

クエリ要求はサポートされていません。

OID_TCP_OFFLOAD_PARAMETERS OID は、set 要求として、ミニポートアダプターの現在の TCP オフロード構成を設定します。 プロトコルドライバーまたはユーザーモードアプリケーションは、この OID を設定して、現在の TCP オフロード構成を変更できます。 システム管理者は、この OID を Microsoft Windows Management Instrumentation (WMI) インターフェイスで使用できます。

## <a name="remarks"></a>注釈

OID_TCP_OFFLOAD_PARAMETERS は、TCP オフロードをサポートするミニポートドライバーと、他のミニポートドライバーでは省略可能です。 ミニポートドライバーがこの OID をサポートしていない場合、ドライバーは NDIS_STATUS_NOT_SUPPORTED を返します。

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体が含まれています。 **Informationbuffer**の内容が無効である場合、ミニポートドライバーは、この OID に応答して NDIS_STATUS_INVALID_DATA を返す必要があります。

この OID は NDIS によって処理され、ミニポートドライバーに OID が渡される前に、NDIS によって、ミニポートアダプターのオフロード標準化されたキーワードが新しい設定で更新されます。

ミニポートドライバーは、 [NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体の内容を使用して、現在報告されている TCP オフロード機能を更新する必要があります。 更新後、ミニポートドライバーは、現在のタスクオフロード機能を[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)ステータスを示す情報と共に報告する必要があります。 この状態の表示により、すべてのプロトコルドライバーが新機能の情報で更新されます。

この OID は、特定のオフロードをオンまたはオフにするようにミニポートドライバーに指示する、より包括的な OID です。 ほとんどの TCP/IP タスクのオフロードは、この OID で構成およびアクティブ化できます。 Rx チェックサムや Rx IPSec など、一部のオフロードでは、この OID は構成の変更として機能し、オフロードはすぐには動作しないという意味ではありません。 これらのオフロードをアクティブにするには、ミニポートドライバーが[OID_OFFLOAD_ENCAPSULATION](oid-offload-encapsulation.md) Set 要求を受信するまで待機する必要があります。

OID_TCP_OFFLOAD_PARAMETERS を設定する前に、アプリケーションまたはドライバーが[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md) OID を使用して、ミニポートアダプターのハードウェアでサポートできる機能を決定できます。 OID_TCP_OFFLOAD_PARAMETERS を使用して、 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md) OID によって無効として報告される機能を有効にします。

### <a name="see-also"></a>関連項目

[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)  
[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |


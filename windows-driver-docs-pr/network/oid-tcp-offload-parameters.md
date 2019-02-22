---
title: OID_TCP_OFFLOAD_PARAMETERS
description: このトピックでは、OID_TCP_OFFLOAD_PARAMETERS オブジェクト識別子 (OID) について説明します。
ms.assetid: 5D9B5F62-E506-4983-B247-A93B81E70A43
keywords:
- OID_TCP_OFFLOAD_PARAMETERS、WDK の Oid、WDK のオブジェクト識別子では、WDK の Oid をネットワークのネットワーク
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: be54f424f8b0d421e046f6bf7a495cd8fe01cd61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552422"
---
# <a name="oidtcpoffloadparameters"></a>OID_TCP_OFFLOAD_PARAMETERS

クエリ要求はサポートされていません。

セットの要求として OID_TCP_OFFLOAD_PARAMETERS OID はミニポート アダプターの現在の TCP オフロードの構成を設定します。 プロトコル ドライバーまたはユーザー モード アプリケーションでは、現在の TCP オフロードの構成を変更するには、この OID を設定できます。 システム管理者は、この OID を使用して、Microsoft Windows Management Instrumentation (WMI) インターフェイスを使用できます。

## <a name="remarks"></a>注釈

OID_TCP_OFFLOAD_PARAMETERS は TCP オフロードをサポートするミニポート ドライバーに必要なその他のミニポート ドライバーでは省略可能です。 ミニポート ドライバーがこの OID をサポートしていない場合、ドライバーは NDIS_STATUS_NOT_SUPPORTED を返す必要があります。

**InformationBuffer**のメンバー、 [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)構造体。 場合の内容**InformationBuffer**は無効ですが、ミニポート ドライバーは、この OID への応答で NDIS_STATUS_INVALID_DATA を返す必要があります。

NDIS この OID を処理すると、NDIS ミニポート アダプターの更新プログラムのミニポート ドライバーに OID が渡される、前に、新しい設定で標準化されたキーワードの負荷を軽減します。

ミニポート ドライバーの内容を使用する必要があります、 [NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)オフロード機能の報告される現在の TCP を更新する構造体。 ミニポート ドライバーの更新後では、現在のタスク オフロード機能を報告する必要があります、 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状態を示す値。 この状態を示す値により、新しい機能の情報ですべての上位のプロトコルのドライバーが更新されるようになります。

この OID は、特定のオフロードを有効または無効にするミニポート ドライバーに指示するより包括的な OID です。 ほとんどの TCP/IP タスク オフロードを構成およびこの OID を使用してアクティブ化できます。 Rx チェックサムまたは Rx の IPSec などのいくつかのオフロードには、この OID は、構成の変更として機能し、オフロードがあります直ちにとは限りません。 これらのオフロードをアクティブ化する、ミニポート ドライバーを受信するまで待つ必要があります、 [OID_OFFLOAD_ENCAPSULATION](oid-offload-encapsulation.md)セットの要求。

上位のアプリケーションまたはドライバーを使用できる OID_TCP_OFFLOAD_PARAMETERS を設定する前に、 [OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)ミニポート アダプターのハードウェアでサポートできるどのような機能を決定する OID。 使用 OID_TCP_OFFLOAD_PARAMETERS 報告される機能を有効にして有効にしないように、 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md) OID。

### <a name="see-also"></a>関連項目

[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)  
[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


---
title: OID_TCP_TASK_OFFLOAD
description: このトピックでは、OID_TCP_TASK_OFFLOAD オブジェクト識別子 (OID) について説明します。
ms.assetid: 4e16cdb7-b899-43b6-a94b-d691622be105
keywords:
- OID_TCP_TASK_OFFLOAD
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85a5b7920351589b5b0043fa581004223763f116
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353697"
---
# <a name="oidtcptaskoffload"></a>OID_TCP_TASK_OFFLOAD

ホスト スタック クエリ、TCP を取得する OID_TCP_TASK_OFFLOAD OID は、ミニポート ドライバーの NIC またはオフロード対象の機能をオフロードします。 NIC またはオフロード ターゲットをサポートする、オフロード機能を決定した後は、ホストのスタックは、1 つ以上の報告機能を有効にするには、この OID を設定します。 ホスト スタックもすべての NIC を無効にするか、オフロード対象の TCP オフロード機能を OID_TCP_TASK_OFFLOAD を設定します。 一度に 1 つだけのプロトコルには、特定の NIC の TCP オフロード機能が有効にすることができます。

## <a name="querying-offload-capabilities"></a>オフロード機能のクエリを実行します。

ホスト スタック OID_TCP_TASK_OFFLOAD を照会する際の提供、 *InformationBuffer* 、 [NDIS_TASK_OFFLOAD_HEADER](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559004(v=vs.85))構造体。 この構造体では、次の項目を指定します。

- ホストのスタックでサポートされているオフロード バージョンです。
- カプセル化形式は、ホストのスタックによって処理されたパケットを送受信します。
- このようなパケット カプセル化ヘッダーのサイズ。

この情報により、ミニポート ドライバーまたはその NIC は、オフロード タスクを実行するための前提条件である送信パケットの最初の IP ヘッダーの先頭を特定できます。 カプセル化形式を把握する必要があります、オフロード対象プロセスがパケットを受信します。 OID_TCP_TASK_OFFLOAD のクエリに応答して、ミニポート ドライバーまたはオフロード ターゲットを返しますで、 *InformationBuffer*、NDIS_TASK_OFFLOAD_HEADER 構造直後に 1 つまたは複数[NDIS_TASK_オフロード](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff558995(v=vs.85))構造体。 各 NDIS_TASK_OFFLOAD 構造体には、ミニポート ドライバーの NIC またはオフロード ターゲット サポート、オフロード機能について説明します。 ミニポート ドライバーの NIC または、オフロード対象のサポート、オフロード機能を複数のバージョン、特定のバージョンごとに 1 つの NDIS_TASK_OFFLOAD 構造体を返す必要があります。

各 NDIS_TASK_OFFLOAD 構造体が、**タスク**特定を指定するメンバーが構造を適用する機能をオフロードします。 各 NDIS_TASK_OFFLOAD 構造があります、 **TaskBuffer**指定したオフロード機能に関連する情報を格納します。 内の情報、 **TaskBuffer**の形式は次の構造体のいずれかです。

- [NDIS_TASK_TCP_IP_CHECKSUM](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559004(v=vs.85))  
    チェックサム オフロード機能を指定します。
- [NDIS_TASK_IPSEC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff558990(v=vs.85))  
    インターネット プロトコル セキュリティ (IPsec) のオフロード機能を指定します。
- [NDIS_TASK_TCP_LARGE_SEND](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559008(v=vs.85))  
    大きな TCP パケットのセグメント化機能を指定します。
- [NDIS_TASK_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_tcp_connection_offload_parameters)  
    TCP chimney オフロード機能を指定します。 NDIS_TASK_TCP_CONNECTION_OFFLOAD の詳細については、次を参照してください。 [TCP Chimney オフロード](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)します。

> [!NOTE]
> 中間ドライバーが、状態の OID_TCP_TASK_OFFLOAD クエリに応答する必要があります、中間ドライバーでは、パケットに対して TCP オフロード機能を実行できませんされるように基になるミニポート ドライバーに転送するパケットの内容を変更する場合NDIS_STATUS_NOT_SUPPORTED OID を渡す代わりには、基になるミニポート ドライバーへの要求またはターゲットの負荷を軽減します。

## <a name="enabling-offload-capabilities"></a>オフロード機能を有効にします。

オフロード機能、NIC のまたはオフロード対象のクエリを実行した後、ホスト スタック OID_TCP_TASK_OFFLOAD を設定してこれらの機能の 1 つ以上を使用します。 OID_TCP_TASK_OFFLOAD を設定するときに、ホストのスタックを提供で、 *InformationBuffer*、NDIS_TASK_OFFLOAD_HEADER 構造体の直後でオフロード機能ごとの NDIS_TASK_OFFLOAD 構造体をホストスタックを有効にします。

**タスク**各 NDIS_TASK_OFFLOAD では、構造体は、オフロード機能ホスト スタックが有効にすることをことを示します。 ホストのスタックもで構造体のメンバーを設定して、特定の特定の側面のオフロード機能により、 **TaskBuffer**各 NDIS_TASK_OFFLOAD 構造体の。

## <a name="changing-offload-capabilities"></a>オフロード機能を変更します。 

NIC またはオフロード ターゲットを有効になっているオフロード機能を変更するには、ホストのスタックは OID_TCP_TASK_OFFLOAD を設定します。 ミニポート ドライバーまたはオフロード ターゲットは、最新 OID_TCP_TASK_OFFLOAD のセットで指定された機能をオフロードもののみに有効にする必要があります。 ミニポート ドライバーまたはオフロード ターゲットは、その他のすべてのオフロード機能を無効にする必要があります。 特定の TCP chimney オフロード機能を無効にすると前に、のホスト スタックが終了機能を使用する任意のオフロードの TCP 接続のオフロードに注意してください。

再開の問題の報告された TCP オフロード機能を変更する負荷を軽減または、オフロード対象が一時停止を使用できます。

- により、一時停止を示す値を呼び出すことによって、オフロード対象、 [NdisMIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex) 、NDIS_STATUS_INDICATION で関数を ->**StatusCode**メンバー NDIS_STATUS_OFFLOAD_PAUSE に設定します。
- により、再開を示す値を呼び出すことによって、オフロード対象、 **NdisMIndicateStatusEx** 、NDIS_STATUS_INDICATION で関数を ->**StatusCode**メンバー NDIS_STATUS_OFFLOAD_RESUME に設定します。

オフロード対象が再開状態オブジェクトをオフロードするホストのスタックを要求した後、オフロード対象の TCP を取得するためにもう一度 OID_TCP_TASK_OFFLOAD ホスト スタック クエリは変更後の機能をオフロードします。 詳細については、次を参照してください。 [NDIS_STATUS_OFFLOAD_RESUME](https://docs.microsoft.com/windows-hardware/drivers/network/)します。

## <a name="disabling-offload-capabilities"></a>オフロード機能を無効にします。

NIC にオフロード ターゲットでサポートされるすべてのオフロード機能を無効にするのには、ホスト スタックは OID_TCP_TASK_OFFLOAD を設定します。 *InformationBuffer*、ホストのスタックで NDIS_TASK_OFFLOAD_HEADER 構造体を提供する、 **OffsetFirstTask**この構造体のメンバーが 0 に設定します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


---
title: OID_TCP_TASK_OFFLOAD
description: このトピックでは、OID_TCP_TASK_OFFLOAD オブジェクト識別子 (OID) について説明します。
ms.assetid: 4e16cdb7-b899-43b6-a94b-d691622be105
keywords:
- OID_TCP_TASK_OFFLOAD
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: f93d2fb8e52654f67c2c686c04e9f265c2c837c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843881"
---
# <a name="oid_tcp_task_offload"></a>OID_TCP_TASK_OFFLOAD

ホストスタックは OID_TCP_TASK_OFFLOAD OID に対してクエリを行い、ミニポートドライバーの NIC またはオフロードターゲットの TCP オフロード機能を取得します。 NIC またはオフロードターゲットでサポートされているオフロード機能を確認した後、ホストスタックは、報告された1つ以上の機能を有効にするために、この OID を設定します。 ホストスタックは、OID_TCP_TASK_OFFLOAD を設定することによって、すべての NIC またはオフロードターゲットの TCP オフロード機能を無効にすることもできます。 特定の NIC の TCP オフロード機能を有効にできるのは、一度に1つのプロトコルのみです。

## <a name="querying-offload-capabilities"></a>オフロード機能のクエリ

ホストスタックでクエリが OID_TCP_TASK_OFFLOAD されると、 *Informationbuffer*に[NDIS_TASK_OFFLOAD_HEADER](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559004(v=vs.85))構造体が提供されます。 この構造体は、次のものを指定します。

- ホストスタックでサポートされているオフロードバージョン。
- ホストスタックによって処理されるパケットを送信および受信するためのカプセル化形式。
- このようなパケット内のカプセル化ヘッダーのサイズ。

この情報を使用すると、ミニポートドライバーまたはその NIC は、送信パケット内の最初の IP ヘッダーの先頭を見つけることができます。これは、オフロードタスクを実行するための前提条件です。 オフロードターゲットは、受信パケットを処理するためのカプセル化形式を認識している必要があります。 OID_TCP_TASK_OFFLOAD のクエリに応答して、ミニポートドライバーまたはオフロードターゲットは、 *Informationbuffer*内の NDIS_TASK_OFFLOAD_HEADER 構造体の直後に1つ以上の[NDIS_TASK_OFFLOAD](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff558995(v=vs.85))構造体を返します。 各 NDIS_TASK_OFFLOAD 構造体は、ミニポートドライバーの NIC またはオフロードターゲットによってサポートされるオフロード機能を記述します。 ミニポートドライバーの NIC またはオフロードのターゲットが、特定のオフロード機能の複数のバージョンをサポートしている場合、各バージョンに対して1つの NDIS_TASK_OFFLOAD 構造を返す必要があります。

各 NDIS_TASK_OFFLOAD 構造体には、構造が適用される特定のオフロード機能を指定する**タスク**メンバーがあります。 各 NDIS_TASK_OFFLOAD 構造体には、指定されたオフロード機能に関連する情報を含む**Taskbuffer**もあります。 **Taskbuffer**内の情報は、次の構造のいずれかとして書式設定されます。

- [NDIS_TASK_TCP_IP_CHECKSUM](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559004(v=vs.85))  
    チェックサムオフロード機能を指定します。
- [NDIS_TASK_IPSEC](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff558990(v=vs.85))  
    インターネットプロトコルセキュリティ (IPsec) オフロード機能を指定します。
- [NDIS_TASK_TCP_LARGE_SEND](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559008(v=vs.85))  
    大きな TCP パケットセグメンテーション機能を指定します。
- [NDIS_TASK_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_tcp_connection_offload_parameters)  
    TCP chimney オフロード機能を指定します。 NDIS_TASK_TCP_CONNECTION_OFFLOAD の詳細については、「 [TCP Chimney オフロード](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)」を参照してください。

> [!NOTE]
> 中間ドライバーが、基になるミニポートドライバーに転送するパケットの内容を変更して、TCP オフロード機能をパケットで実行できない場合、中間ドライバーは、状態が OID_TCP_TASK_OFFLOAD のクエリに応答する必要があります。基になるミニポートドライバーまたはオフロードターゲットに OID 要求を渡す代わりに NDIS_STATUS_NOT_SUPPORTED。

## <a name="enabling-offload-capabilities"></a>オフロード機能の有効化

NIC またはオフロードターゲットのオフロード機能に対してクエリを実行した後、ホストスタックは OID_TCP_TASK_OFFLOAD を設定することによって、これらの機能の1つ以上を有効にします。 OID_TCP_TASK_OFFLOAD を設定すると、ホストスタックは、NDIS_TASK_OFFLOAD_HEADER 構造*体の後*に、ホストスタックで有効になっているオフロード機能ごとに NDIS_TASK_OFFLOAD 構造体の直後にある構造体を提供します。

各 NDIS_TASK_OFFLOAD 構造体の**タスク**は、ホストスタックが有効になっているオフロード機能を示します。 また、ホストスタックは、各 NDIS_TASK_OFFLOAD 構造体の**Taskbuffer**で構造体のメンバーを設定することによって、特定のオフロード機能の特定の側面を有効にします。

## <a name="changing-offload-capabilities"></a>オフロード機能の変更 

NIC またはオフロードターゲットに対して有効になっているオフロード機能を変更するために、ホストスタックは OID_TCP_TASK_OFFLOAD を設定します。 ミニポートドライバーまたはオフロードターゲットでは、最新の OID_TCP_TASK_OFFLOAD セットによって指定されたオフロード機能のみを有効にする必要があります。 ミニポートドライバーまたはオフロードターゲットでは、その他のオフロード機能をすべて無効にする必要があります。 特定の TCP chimney オフロード機能を無効にする前に、ホストスタックは、その機能を使用するオフロードされた TCP 接続のオフロードを終了します。

オフロードターゲットでは、一時停止または再開オフロードの表示を使用して、報告される TCP オフロード機能を変更できます。

- オフロードターゲットは、NDIS_STATUS_INDICATION >**StatusCode**メンバーが NDIS_STATUS_OFFLOAD_PAUSE に設定された[NdisMIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数を呼び出すことにより、一時停止を示します。
- オフロードターゲットは、NDIS_STATUS_INDICATION >**StatusCode**メンバーが NDIS_STATUS_OFFLOAD_RESUME に設定された**NdisMIndicateStatusEx**関数を呼び出すことにより、再開を示します。

オフロードターゲットによって、状態オブジェクトのオフロードを再開するように要求された後、ホストスタックはもう一度 OID_TCP_TASK_OFFLOAD を実行して、オフロードターゲットの TCP オフロードの変更された機能を取得します。 詳細については、「 [NDIS_STATUS_OFFLOAD_RESUME](https://docs.microsoft.com/windows-hardware/drivers/network/)」を参照してください。

## <a name="disabling-offload-capabilities"></a>オフロード機能の無効化

NIC またはオフロードターゲットでサポートされているオフロード機能をすべて無効にするには、ホストスタックで OID_TCP_TASK_OFFLOAD を設定します。 *Informationbuffer*では、ホストスタックは、この構造体の**OffsetFirstTask**メンバーが0に設定された NDIS_TASK_OFFLOAD_HEADER 構造体を提供します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |


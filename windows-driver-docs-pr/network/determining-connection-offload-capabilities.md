---
title: 接続のオフロード機能の決定
description: 接続のオフロード機能の決定
ms.assetid: 9a7c40dd-7151-462f-b30b-0444a4177ff9
keywords:
- 接続オフロード WDK TCP/IP トランスポート、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c2dec3eb0bf58f82a85be6bc0c24f430850f61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838149"
---
# <a name="determining-connection-offload-capabilities"></a>接続のオフロード機能の決定





NDIS では、2つのカテゴリのオフロードサービスがサポートされています。 TCP/IP オフロードサービスは、NDIS 5.1 以前のタスクオフロードサービスと接続オフロードサービスの拡張形式です。

NDIS は、負荷の軽減ハードウェア機能と、基になるミニポートアダプターの現在の構成を[**ndis\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体のプロトコルドライバーに提供します。 NDIS には、タスクのオフロードハードウェア機能と、基になるミニポートアダプターの現在の構成が用意されています。これにより、 [**ndis\_フィルター\_\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体にフィルターを適用できます。

管理アプリケーションは、オブジェクト識別子 (OID) クエリを使用して、ミニポートアダプターの TCP/IP オフロード機能を取得します。 ただし、それ以上のドライバーは OID クエリを使用しないようにする必要があります。 プロトコルドライバーは、基になるドライバーによって報告される TCP/IP オフロード機能の変更を処理する必要があります。 ミニポートドライバーは、ステータスを示す状態のタスクオフロード機能の変更を報告できます。 ステータスの表示の一覧については、「 [NDIS Tcp/ip オフロードの状態](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)の表示」を参照してください。

管理アプリケーション (またはそれ以降のドライバー) では、 [OID\_TCP\_接続\_オフロード\_現在の\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)OID に対してクエリを実行することで、NIC の現在の接続のオフロード構成を特定できます。 [**NDIS\_tcp\_接続\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) 、OID に関連付けられているオフロード構造の\_TCP\_接続\_オフロード\_現在の\_CONFIG は、ミニポートアダプターの現在の構成を指定します。接続オフロードの構成。

 

 






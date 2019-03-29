---
title: タスク オフロード機能の判断
description: タスク オフロード機能の判断
ms.assetid: 9348a595-7bc0-467e-aeaf-e23100c99524
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7043cb69470aa43e0403ff7238788c8ad23bd585
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573741"
---
# <a name="determining-task-offload-capabilities"></a>タスク オフロード機能の判断





NDIS 5.1 と前のタスクの強化されたフォームである NDIS サポート タスク オフロード サービスは、サービスをオフロードします。 オフロード機能の接続を確認する方法の詳細については、「[接続オフロード機能を決定する](determining-connection-offload-capabilities.md)します。

NDIS オフロードのハードウェア機能とプロトコル ドライバーで基になるミニポート アダプターの現在の構成を提供する、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。 NDIS フィルター ドライバーで基になるミニポート アダプターの現在の構成とタスク オフロードのハードウェア機能を提供します、 [ **NDIS\_フィルター\_アタッチ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。

管理アプリケーションでは、オブジェクト識別子 (OID) のクエリを使用して、ミニポート アダプターのタスクのオフロード機能を取得します。 ただし、後続のドライバーには、OID のクエリを使用しないでください。 プロトコル ドライバーでは、その基になるドライバー レポート タスクのオフロード機能に変更を処理する必要があります。 ミニポート ドライバーでは、タスクの変更のオフロードで状態インジケーターの機能をレポートできます。 状態インジケーターの一覧は、次を参照してください。 [NDIS 6.0 TCP/IP Offload 状態インジケーター](https://msdn.microsoft.com/library/windows/hardware/ff567880)します。

管理アプリケーション (または上にあるドライバー) は、クエリを実行してネットワーク インターフェイス カード (NIC) の現在のタスク オフロードの構成を決定できます、 [OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805) OID。

[ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599)構造に関連付けられている[OID\_TCP\_オフロード\_現在\_構成](https://msdn.microsoft.com/library/windows/hardware/ff569805)次を指定します。

-   ヘッダーは、TCP/IP トランスポートをサポートするタスクのオフロード バージョンが含まれています。

-   チェックサムでは、負荷を軽減する[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)構造体。

-   大規模なオフロード バージョン 1 (LSOV1) を送信する情報で、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff567883)構造体。

-   インターネット プロトコル セキュリティ (IPsec) については、ので、 [ **NDIS\_IPSEC\_オフロード\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff565796)構造体。

-   大規模なオフロード バージョン 2 (LSOV2) を送信する情報で、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff567884)構造体。

-   インターネット プロトコル セキュリティ (IPsecvOV) 情報、 [ **NDIS\_IPSEC\_オフロード\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff565808)構造体。

次のトピックでは、オフロード サービスの種類ごとに固有の情報を紹介します。

-   [NIC のチェックサム機能の報告](reporting-a-nic-s-checksum-capabilities.md)
-   [レポートの NIC の LSOV1 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)
-   [レポートの NIC の LSOV2 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)
-   [NIC の IPsec の機能の報告](reporting-a-nic-s-ipsec-capabilities.md)
    - \[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

 

 






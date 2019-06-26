---
title: 接続オフロード機能の判断
description: 接続オフロード機能の判断
ms.assetid: 9a7c40dd-7151-462f-b30b-0444a4177ff9
keywords:
- 接続は、WDK TCP/IP トランスポート、機能をオフロードします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1764ed2d0d8453aaa602055e6158ad786b24bf4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381432"
---
# <a name="determining-connection-offload-capabilities"></a>接続オフロード機能の判断





NDIS は、オフロード サービスの 2 つのカテゴリをサポートしています。TCP/IP は、NDIS 5.1 と以前のタスクのオフロード サービスの強化されたフォームであるサービスと接続のオフロード サービスをオフロードします。

NDIS オフロードのハードウェア機能とプロトコル ドライバーで基になるミニポート アダプターの現在の構成を提供する、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体。 NDIS フィルター ドライバーで基になるミニポート アダプターの現在の構成とタスク オフロードのハードウェア機能を提供します、 [ **NDIS\_フィルター\_アタッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体。

管理アプリケーションでは、オブジェクト識別子 (OID) のクエリを使用して、ミニポート アダプターの TCP/IP のオフロード機能を取得します。 ただし、後続のドライバーには、OID のクエリを使用しないでください。 プロトコル ドライバーでは、その基になるドライバー レポート TCP/IP のオフロード機能に変更を処理する必要があります。 ミニポート ドライバーでは、タスクの変更のオフロードで状態インジケーターの機能をレポートできます。 状態インジケーターの一覧は、次を参照してください。 [NDIS TCP/IP Offload 状態インジケーター](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)します。

管理アプリケーション (または上にあるドライバー) は、クエリを実行して、NIC の現在の接続オフロードの構成を確認できます、 [OID\_TCP\_接続\_オフロード\_現在\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config) OID。 [ **NDIS\_TCP\_接続\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) OID に関連付けられている構造\_TCP\_接続\_オフロード\_現在\_CONFIG ミニポート アダプターの現在の接続オフロードの構成を指定します。

 

 






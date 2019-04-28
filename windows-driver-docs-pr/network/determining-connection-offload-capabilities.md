---
title: 接続オフロード機能の判断
description: 接続オフロード機能の判断
ms.assetid: 9a7c40dd-7151-462f-b30b-0444a4177ff9
keywords:
- 接続は、WDK TCP/IP トランスポート、機能をオフロードします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7586ca5a2ccfbf94b68c95411dd3b1ebb443cd8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364220"
---
# <a name="determining-connection-offload-capabilities"></a>接続オフロード機能の判断





NDIS は、オフロード サービスの 2 つのカテゴリをサポートしています。TCP/IP は、NDIS 5.1 と以前のタスクのオフロード サービスの強化されたフォームであるサービスと接続のオフロード サービスをオフロードします。

NDIS オフロードのハードウェア機能とプロトコル ドライバーで基になるミニポート アダプターの現在の構成を提供する、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。 NDIS フィルター ドライバーで基になるミニポート アダプターの現在の構成とタスク オフロードのハードウェア機能を提供します、 [ **NDIS\_フィルター\_アタッチ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。

管理アプリケーションでは、オブジェクト識別子 (OID) のクエリを使用して、ミニポート アダプターの TCP/IP のオフロード機能を取得します。 ただし、後続のドライバーには、OID のクエリを使用しないでください。 プロトコル ドライバーでは、その基になるドライバー レポート TCP/IP のオフロード機能に変更を処理する必要があります。 ミニポート ドライバーでは、タスクの変更のオフロードで状態インジケーターの機能をレポートできます。 状態インジケーターの一覧は、次を参照してください。 [NDIS TCP/IP Offload 状態インジケーター](https://msdn.microsoft.com/library/windows/hardware/ff567880)します。

管理アプリケーション (または上にあるドライバー) は、クエリを実行して、NIC の現在の接続オフロードの構成を確認できます、 [OID\_TCP\_接続\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569802) OID。 [ **NDIS\_TCP\_接続\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567875) OID に関連付けられている構造\_TCP\_接続\_オフロード\_現在\_CONFIG ミニポート アダプターの現在の接続オフロードの構成を指定します。

 

 






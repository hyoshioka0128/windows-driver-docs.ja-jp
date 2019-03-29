---
title: Windows ソケット アプリケーションでの SAN の使用
description: Windows ソケット アプリケーションでの SAN の使用
ms.assetid: 140505dd-2e3c-48b2-94c0-911ea460068c
keywords:
- システム エリア ネットワーク WDK、Windows ソケット アプリケーション
- SAN の WDK、Windows ソケット アプリケーション
- Windows Sockets applications WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e08d778e15989f6ced0e87f310b6569b4791151
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581218"
---
# <a name="using-a-san-with-windows-sockets-applications"></a>Windows ソケット アプリケーションでの SAN の使用





Windows ソケット アプリケーションは、システム エリア ネットワーク (SAN) を使用してから利用できます。 これらのアプリケーションでは、一括形式のデータを転送し、コピーと呼ばれるテクノロジを使用して、ユーザーのカーネルの境界を越えてせず、SAN ネットワークに直接データを削除するに SAN を使用できる[Windows Sockets 直接](windows-sockets-direct.md)します。 Windows Sockets ダイレクトではこれらのアプリケーションを透過的に SAN を使用できます。

Windows ソケット アプリケーションごとに、Windows Sockets 直接ことができますか。

-   SAN に直接の SAN 経由で流れるデータ トラフィックをルーティングします。

    システム提供の Windows ソケットは、SAN、ネットワーク経由で転送される SAN NIC に直接 Windows ソケット アプリケーションから発信された SAN の Windows Sockets ダイレクト ルート データ トラフィックのコンポーネントを切り替えます。 スイッチでは、その SAN の特定の Windows Sockets サービス プロバイダーを使用して、データを転送します。

-   TCP/IP 経由の他のネットワーク経由で送信するデータ トラフィックをルーティングします。

    Windows ソケット アプリケーションから特定の SAN のないデータ トラフィックをルーティングするには、スイッチは、TCP/IP サービス プロバイダーを使用する必要があります。 非固有 SAN のデータ トラフィックが含まれています、たとえば、データグラム、マルチキャスト、および接続をルーティングする必要があります。 非固有 SAN のデータ トラフィックが TCP/IP および SAN nic の NDIS ミニポート ドライバー経由でルーティングし、

 

 






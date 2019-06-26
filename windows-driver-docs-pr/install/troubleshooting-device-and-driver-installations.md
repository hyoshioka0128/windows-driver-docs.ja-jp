---
title: デバイスとドライバーのインストールのトラブルシューティング
description: デバイスとドライバーのインストールのトラブルシューティング
ms.assetid: 1ffad62b-140d-4a0a-9174-245e0344e605
keywords:
- トラブルシューティング、デバイス セットアップ WDK デバイス インストール
- デバイスのインストール、WDK のトラブルシューティング
- WDK、デバイスのインストールのトラブルシューティング
- WDK のデバイス インストールのトラブルシューティング
- デバイス セットアップ WDK デバイスのインストール、SetupAPI
- デバイス、WDK SetupAPI をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff801448db37d9ddb27ed0dbc7b6d38f7a684254
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371280"
---
# <a name="troubleshooting-device-and-driver-installations"></a>デバイスとドライバーのインストールのトラブルシューティング





デバイスが正しくインストールされていることを確認します。 または、デバイスのインストールに関する問題の診断には、次のガイドラインを使用できます。

-   記載されている手順に従います[デバイス マネージャーを使用して](using-device-manager.md)デバイスに関するシステム情報を表示します。

-   記載されている手順に従います[(Windows Vista 以降) は、SetupAPI ログ](setupapi-logging--windows-vista-and-later-.md)または[(Windows Server 2003、Windows XP、および Windows 2000) は、SetupAPI ログ](setupapi-logging--windows-server-2003--windows-xp--and-windows-2000-.md)インストール エラーを特定します。

-   Windows Vista および Windows の以降のバージョンでは、上で説明されている手順に従います[(Windows Vista 以降) デバイス インストールのデバッグ](debugging-device-installations--windows-vista-and-later-.md)をデバッグする[co-installer](writing-a-co-installer.md)デバイスの主要な段階インストールします。

-   Windows Vista および Windows の以降のバージョンでは、上で説明されている手順に従います[インストールのトラブルシューティングとテスト署名されたドライバーと負荷の問題](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)関連の問題を診断するインストールとテスト署名の読み込みドライバーです。

-   デバイスの実行にテスト プログラムを実行します。 これには、Windows Driver Kit (WDK) で提供されるテストおよびデバッグ ツールが含まれます。

Windows Server 2003、Windows XP、および Windows 2000 では、さらで、[共同インストーラー](writing-a-co-installer.md)ユーザー、デバイスに関する問題の診断に役立つトラブルシューティング ツールを提供することができます。 参照してください[ **DIF_TROUBLESHOOTER** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-troubleshooter)詳細についてはします。

 

 






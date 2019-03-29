---
title: ファイル システム ドライバーのインストール
description: ファイル システム ドライバーのインストール
ms.assetid: 1297b565-ac85-4248-927a-ab91b6cb3ab0
keywords:
- ドライバー WDK ファイル システムをインストールします。
- ファイル システム ドライバー WDK をインストールします。
- INF ファイル WDK ファイル システム
- INF ファイルをファイル システム ドライバーのインストールについての WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a055607d6e59246990408ab44806b15fd0af4606
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582477"
---
# <a name="installing-a-file-system-driver"></a>ファイル システム ドライバーのインストール


## <span id="ddk_installing_a_file_system_filter_driver_if"></span><span id="DDK_INSTALLING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


Microsoft Windows XP と以降のオペレーティング システムでは、INF ファイルと、インストール アプリケーションを使用して、ファイル システム ドライバーをインストールする必要があります。 (Microsoft Windows 2000 および以前のオペレーティング システムでは、ファイル システム ドライバーがよくインストール サービス コントロール マネージャーによって)。

今後、INF ベースのインストールは、ファイル システム ドライバー用の Windows ハードウェア認定キットの要件を満たしていると想定されます。 「INF ベースのインストール」の意味をのみファイルをコピーして、レジストリの情報を格納する INF ファイルを使用する必要がありますに注意してください。 INF ファイルのみを使用して、全体の製品をインストールする必要はありませんし、提供する必要はありません、 [「インストールを右クリックして」](using-an-inf-file-to-install-a-file-system-filter-driver.md)ドライバーのオプション。

このセクションの内容:

[ファイル システム ドライバーの INF ファイルを作成します。](creating-an-inf-file-for-a-file-system-driver.md)

次のセクションは、[ファイル システム フィルター ドライバー](file-system-filter-drivers.md)をインストールして、ファイル システム フィルター ドライバーのアンインストールに関するセクションはもファイル システム ドライバーを適用できます。

[INF ファイルを使用して、ファイル システム フィルター ドライバーをインストールするには](using-an-inf-file-to-install-a-file-system-filter-driver.md)

[ファイル システム フィルター ドライバーをアンインストールする INF ファイルを使用します。](using-an-inf-file-to-uninstall-a-file-system-filter-driver.md)

 

 





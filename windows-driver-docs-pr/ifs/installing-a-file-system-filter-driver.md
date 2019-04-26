---
title: ファイル システム フィルター ドライバーのインストール
description: ファイル システム フィルター ドライバーのインストール
ms.assetid: c8a7fd20-8baa-449a-afa6-9692da706df4
keywords:
- フィルター ドライバー WDK のファイル システムをインストールします。
- ファイル システム フィルター ドライバー WDK をインストールします。
- INF ファイル WDK ファイル システム
- INF ファイル WDK ファイル システム、ファイル システム フィルター ドライバーのインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0628a09a805f99c83f3aefafc7972a4f3003293
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357574"
---
# <a name="installing-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーのインストール


## <span id="ddk_installing_a_file_system_filter_driver_if"></span><span id="DDK_INSTALLING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


Microsoft Windows XP と以降のオペレーティング システムでは、INF ファイルと、インストール アプリケーションを使用して、ファイル システム フィルター ドライバーをインストールする必要があります。 (Windows 2000 および以前のオペレーティング システムでは、フィルター ドライバーがよくインストール サービス コントロール マネージャーによって)。

今後、INF ベースのインストールは、ファイル システム フィルター ドライバーの Windows ハードウェア認定キットの要件を満たしていると想定されます。 「INF ベースのインストール」の意味をのみファイルをコピーして、レジストリの情報を格納する INF ファイルを使用する必要がありますに注意してください。 INF ファイルのみを使用して、全体の製品をインストールする必要はありませんし、提供する必要はありません、 [「インストールを右クリックして」](using-an-inf-file-to-install-a-file-system-filter-driver.md)ドライバーのオプション。

このセクションの内容:

[ファイル システム フィルター ドライバーの INF ファイルを作成します。](creating-an-inf-file-for-a-file-system-filter-driver.md)

[ファイル システム フィルター ドライバーの読み込み順序グループ](load-order-groups-for-file-system-filter-drivers.md)

[ファイル システム フィルター ドライバーのクラスおよびクラスの Guid](file-system-filter-driver-classes-and-class-guids.md)

[INF ファイルを使用して、ファイル システム フィルター ドライバーをインストールするには](using-an-inf-file-to-install-a-file-system-filter-driver.md)

[ファイル システム フィルター ドライバーをアンインストールする INF ファイルを使用します。](using-an-inf-file-to-uninstall-a-file-system-filter-driver.md)

 

 





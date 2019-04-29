---
title: NDIS フィルター ドライバーのインストール
description: NDIS フィルター ドライバーのインストール
ms.assetid: 8e0c47bf-6b63-4be5-98b7-7a99e9efe283
keywords:
- フィルター ドライバー WDK ネットワー キングのインストール
- NDIS フィルター ドライバー WDK をインストール
- NDIS フィルター ドライバー WDK ネットワークをインストールします。
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 206e50dfadcfb936da190176949e61505d3182b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392923"
---
# <a name="ndis-filter-driver-installation"></a>NDIS フィルター ドライバーのインストール

このセクションでは、NDIS フィルター ドライバーのインストールに関する情報を提供します。 軽量のフィルター ドライバーは、中間のフィルター ドライバーと異なります。 Configuration manager では、各ミニポート アダプター用のフィルター モジュールの一覧で NDIS が用意されています。 ない仮想デバイス (または仮想ミニポート) NDIS 中間フィルター ドライバーの場合のように、フィルター ドライバーと関連付けられています。

フィルター ドライバーをインストールするには、1 つの INF ファイルを提供する必要があります。 Configuration manager では、INF ファイルから、フィルター ドライバーに関する構成情報を読み取るし、レジストリにコピーします。

フィルター ドライバーの INF ファイルでは、ネットワーク サービスを定義します。 フィルター ドライバーのミニポート INF ファイルではありません。 例フィルター ドライバーの INF ファイルでは、次を参照してください。、 [ndislwf](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/filter)サンプル ドライバー。

フィルター ドライバーをインストールまたはアンインストールする必要がありますを使用して、フィルター ドライバーの INF ファイルを指定すると、`INetCfg`ファミリの[構成のネットワーク インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v%3dvs.85))します。 たとえば、ネットワークのコンポーネントをインストールまたは削除を呼び出す、 [INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709%28v%3dvs.85%29)インターフェイス。 プログラムによってこれらのインターフェイスを呼び出すことができますか、または直接いないで[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)、呼び出す`INetCfg`できます。 使用することはできません[SetupAPI](../install/setupapi.md)をインストールまたは NDIS フィルター ドライバーをアンインストールします。

呼び出すことの例については`INetCfg`、コードを参照してください、 [Bindview ネットワーク構成ユーティリティ サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/config/bindview)します。

このセクションの内容:

[フィルター ドライバーのバインディングの関係を指定します。](specifying-filter-driver-binding-relationships.md)

[フィルター ドライバーの INF ファイルの設定](inf-file-settings-for-filter-drivers.md)

[フィルター ドライバーの構成情報にアクセスします。](accessing-configuration-information-for-a-filter-driver.md)
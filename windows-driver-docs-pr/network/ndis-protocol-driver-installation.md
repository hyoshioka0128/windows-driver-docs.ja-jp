---
title: NDIS プロトコル ドライバーのインストール
description: NDIS プロトコル ドライバーのインストール
ms.assetid: D783E386-91A2-4E6E-8340-78E0FFA14974
keywords:
- プロトコル ドライバー WDK ネットワー キングのインストール
- NDIS プロトコル ドライバー WDK をインストール
- NDIS プロトコル ドライバー WDK ネットワークをインストールします。
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7c7eca1e6a2c3a86dec3bfae3992877d4398879f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553251"
---
# <a name="ndis-protocol-driver-installation"></a>NDIS プロトコル ドライバーのインストール

プロトコル ドライバーをインストールするには、まず 1 つの INF ファイルを提供する必要があります。 Configuration manager では、プロトコル ドライバーに関する構成情報を INF ファイルから読み取るし、レジストリにコピーします。 

プロトコル ドライバーの INF ファイルの詳細については、[ネットワーク プロトコルのインストール要件](installation-requirements-for-network-protocols.md)を参照してください。 例プロトコル ドライバーの INF ファイルでは、次を参照してください。、 [ndisprot 630](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot/6x/sys/630)サンプル ドライバー。

プロトコルには、ドライバーをインストールまたはアンインストールする必要がありますを使用するには、プロトコル ドライバーの INF ファイルを指定すると、`INetCfg`ファミリの[構成のネットワーク インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v%3dvs.85))します。 たとえば、ネットワークのコンポーネントをインストールまたは削除を呼び出す、 [INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709%28v%3dvs.85%29)インターフェイス。 プログラムによってこれらのインターフェイスを呼び出すことができますか、または直接いないで[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)、呼び出す`INetCfg`できます。 使用することはできません[SetupAPI](../install/setupapi.md)をインストールまたは NDIS プロトコル ドライバーをアンインストールします。

呼び出すことの例については`INetCfg`、コードを参照してください、 [Bindview ネットワーク構成ユーティリティ サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/config/bindview)します。
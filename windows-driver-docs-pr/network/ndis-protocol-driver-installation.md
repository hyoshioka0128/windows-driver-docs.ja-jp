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
ms.openlocfilehash: e61376fdd308b3f295eb881717964702e3d4fe9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369170"
---
# <a name="ndis-protocol-driver-installation"></a>NDIS プロトコル ドライバーのインストール

プロトコル ドライバーをインストールするには、まず 1 つの INF ファイルを提供する必要があります。 Configuration manager では、プロトコル ドライバーに関する構成情報を INF ファイルから読み取るし、レジストリにコピーします。 

プロトコル ドライバーの INF ファイルの詳細については、次を参照してください。[ネットワーク プロトコルのインストール要件](installation-requirements-for-network-protocols.md)します。 例プロトコル ドライバーの INF ファイルでは、次を参照してください。、 [ndisprot 630](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot/6x/sys/630)サンプル ドライバー。

プロトコルには、ドライバーをインストールまたはアンインストールする必要がありますを使用するには、プロトコル ドライバーの INF ファイルを指定すると、`INetCfg`ファミリの[構成のネットワーク インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v=vs.85))します。 たとえば、ネットワークのコンポーネントをインストールまたは削除を呼び出す、 [INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709(v=vs.85))インターフェイス。 プログラムによってこれらのインターフェイスを呼び出すことができますか、または直接いないで[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)、呼び出す`INetCfg`できます。 使用することはできません[SetupAPI](../install/setupapi.md)をインストールまたは NDIS プロトコル ドライバーをアンインストールします。

呼び出すことの例については`INetCfg`、コードを参照してください、 [Bindview ネットワーク構成ユーティリティ サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/config/bindview)します。
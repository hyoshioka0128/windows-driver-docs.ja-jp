---
title: PortDMus DirectMusic ポートの既定のドライバーの作成
description: PortDMus DirectMusic ポートの既定のドライバーの作成
ms.assetid: 1e498eb1-8a48-4240-8557-2fd2bba02abb
keywords:
- ポート ドライバー WDK オーディオ、既定の Dmu ポート ドライバー
- 既定の Dmu ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb7d2a29a7589de2c217b9c8fe14cbeffdb018e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556964"
---
# <a name="making-portdmus-the-default-directmusic-port-driver"></a>PortDMus DirectMusic ポートの既定のドライバーの作成


## <span id="making_portdmus_the_default_directmusic_port_driver"></span><span id="MAKING_PORTDMUS_THE_DEFAULT_DIRECTMUSIC_PORT_DRIVER"></span>


Dmu ポート ドライバーを DirectMusic のすべてのアプリケーションの既定値にするには、(uuidgen.exe または Microsoft Windows SDK に含まれている、guidgen.exe を使用) の GUID を生成、シンセサイザーを一意に識別します。 [ **KSPROPERTY\_シンセサイザー\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff537389)プロパティ ハンドラーには、この GUID をコピーする必要があります、 **Guid**のメンバー、 [ **SYNTHCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff538424)構造体。 また、次のレジストリ エントリを設定するドライバーの INF ファイルを変更します。

```inf
Key:    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\Defaults
String Value:    DefaultOutputPort
```









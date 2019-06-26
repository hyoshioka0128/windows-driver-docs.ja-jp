---
title: PortDMus を既定の DirectMusic ポート ドライバーとする
description: PortDMus を既定の DirectMusic ポート ドライバーとする
ms.assetid: 1e498eb1-8a48-4240-8557-2fd2bba02abb
keywords:
- ポート ドライバー WDK オーディオ、既定の Dmu ポート ドライバー
- 既定の Dmu ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2228bdd862ed280284253e7063ab0fd9a00cbddd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358686"
---
# <a name="making-portdmus-the-default-directmusic-port-driver"></a>PortDMus を既定の DirectMusic ポート ドライバーとする


## <span id="making_portdmus_the_default_directmusic_port_driver"></span><span id="MAKING_PORTDMUS_THE_DEFAULT_DIRECTMUSIC_PORT_DRIVER"></span>


Dmu ポート ドライバーを DirectMusic のすべてのアプリケーションの既定値にするには、(uuidgen.exe または Microsoft Windows SDK に含まれている、guidgen.exe を使用) の GUID を生成、シンセサイザーを一意に識別します。 [ **KSPROPERTY\_シンセサイザー\_CAP** ](https://docs.microsoft.com/previous-versions/ff537389(v=vs.85))プロパティ ハンドラーには、この GUID をコピーする必要があります、 **Guid**のメンバー、 [ **SYNTHCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusprop/ns-dmusprop-_synthcaps)構造体。 また、次のレジストリ エントリを設定するドライバーの INF ファイルを変更します。

```inf
Key:    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\Defaults
String Value:    DefaultOutputPort
```









---
title: PortDMus を既定の DirectMusic ポート ドライバーとする
description: PortDMus を既定の DirectMusic ポート ドライバーとする
ms.assetid: 1e498eb1-8a48-4240-8557-2fd2bba02abb
keywords:
- ポートドライバー WDK オーディオ、既定の DMus ポートドライバー
- 既定の DMus ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f34f667b1f8d01a9474e39f331d0ced0fb303c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830397"
---
# <a name="making-portdmus-the-default-directmusic-port-driver"></a>PortDMus を既定の DirectMusic ポート ドライバーとする


## <span id="making_portdmus_the_default_directmusic_port_driver"></span><span id="MAKING_PORTDMUS_THE_DEFAULT_DIRECTMUSIC_PORT_DRIVER"></span>


すべての DirectMusic アプリケーションの既定値として DMus ポートドライバーを使用するには、(Microsoft Windows SDK に含まれている) uuidgen.exe または guidgen.exe を使用して、シンセを一意に識別する GUID を生成します。 [**Ksk プロパティ\_シンセサイザー\_caps**](https://docs.microsoft.com/previous-versions/ff537389(v=vs.85))プロパティハンドラーは、この Guid を[**synthcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusprop/ns-dmusprop-_synthcaps)構造体の**guid**メンバーにコピーする必要があります。 また、ドライバーの INF ファイルを変更して、次のレジストリエントリを設定します。

```inf
Key:    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\Defaults
String Value:    DefaultOutputPort
```









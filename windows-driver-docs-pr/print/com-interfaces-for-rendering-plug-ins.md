---
title: プラグインを表示するための COM インターフェイス
description: プラグインを表示するための COM インターフェイス
ms.assetid: 3a1a67ed-7c29-42fa-9bd2-ee38468f6d4b
keywords:
- プラグインの WDK の印刷、COM インターフェイスを表示
- WDK の COM インターフェイスを印刷するレンダリング プラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b74e4b2af07f9c1479828842a9795629aec3899
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530902"
---
# <a name="com-interfaces-for-rendering-plug-ins"></a>プラグインを表示するための COM インターフェイス





Microsoft のプリンター ドライバーとレンダリング プラグイン間の通信は、次の COM インターフェイスが定義されています。

[IPrintOemUni COM インターフェイス](iprintoemuni-com-interface.md)、ことができます、[プリンター グラフィックス DLL](printer-graphics-dll.md) Unidrv レンダリング プラグインを呼び出すためです。

[COM インターフェイスの IPrintOemUni2](iprintoemuni2-com-interface.md)、IPrintOemUni COM インターフェイスの機能を拡張します。

[COM インターフェイスの IPrintOemUni3](iprintoemuni3-com-interface.md)IPrintOemUni2 COM インターフェイスや、IPrintOemUni の機能を拡張します。

[COM インターフェイスの IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、Unidrv ユーティリティ操作レンダリング プラグインを提供します。

[IPrintOemPS COM インターフェイス](iprintoemps-com-interface.md)、ことができます、[プリンター グラフィックス DLL](printer-graphics-dll.md) Pscript5 レンダリング プラグインを呼び出すためです。

[COM インターフェイスの IPrintOemPS2](iprintoemps2-com-interface.md)、IPrintOemPS COM インターフェイスの機能を拡張します。

[COM インターフェイスの IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、Pscript5 ユーティリティ操作レンダリング プラグインを提供します。

[COM インターフェイスの IPrintCorePS2](iprintcoreps2-com-interface.md)プラグインをレンダリングする Pscript5 ミニドライバーのヘルパー メソッドが提供されます。

次の図は、レンダリングのプラグインで使用される COM インターフェイスの継承ツリーを示します。

![使用される com インターフェイスの継承ツリーを示す図は、プラグインを表示します。](images/rendintf.png)

 

 





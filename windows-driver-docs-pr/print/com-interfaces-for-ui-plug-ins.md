---
title: UI プラグインの COM インターフェイス
description: UI プラグインの COM インターフェイス
ms.assetid: 9cc6502b-a003-4d0b-857e-4653cf6fa0ea
keywords:
- ユーザー インターフェイスのプラグインの WDK の印刷、COM インターフェイスします。
- UI プラグイン WDK を印刷する COM インターフェイス
- WDK の COM インターフェイスを印刷するユーザー インターフェイスのプラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf15ccce5b96267ded0dce6f0cd73e40c18f957a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528384"
---
# <a name="com-interfaces-for-ui-plug-ins"></a>UI プラグインの COM インターフェイス





Microsoft のプリンター ドライバーと UI プラグイン間の通信は、次の COM インターフェイスが定義されています。

-   [IPrintOemCommon COM インターフェイス](iprintoemcommon-com-interface.md)を指定し、デバイス情報を取得するメソッドを提供します。

-   [IPrintOemUI COM インターフェイス](iprintoemui-com-interface.md)、有効にする、[プリンター インターフェイス DLL](printer-interface-dll.md) Unidrv または Pscript5 UI プラグインを呼び出す。

-   [IPrintOemUI2 COM インターフェイス](iprintoemui2-com-interface.md)、延長、 [IPrintOemUI COM インターフェイス](iprintoemui-com-interface.md)します。

-   [IPrintOemUIMXDC COM インターフェイス](iprintoemuimxdc-com-interface.md)、フィルター パイプラインのドライバーで XPS の出力を呼び出す UI プラグイン GDI から変換を制御することができます。

-   [IPrintOemDriverUI COM インターフェイス](iprintoemdriverui-com-interface.md)、ユーティリティ操作 UI プラグインを提供します。

-   [IPrintCoreUI2 COM インターフェイス](iprintcoreui2-com-interface.md)、UI プラグインがミニドライバーのヘルパー メソッドを提供します。

次の図は、UI プラグインで使用する COM インターフェイスの継承ツリーを示します。

![ui プラグインで使用する com インターフェイスの継承ツリーを示す図](images/uiintf2.png)

 

 





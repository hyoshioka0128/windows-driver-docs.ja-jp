---
title: Gcdef.dll、既定のアナログ デバイスのプロパティ シート
description: Gcdef.dll、既定のアナログ デバイスのプロパティ シート
ms.assetid: a8226abb-11c1-4425-93d8-b74e1960ba10
keywords:
- Gcdef.dll
- 既定のアナログ デバイスのプロパティ シート
- プロパティ シート WDK DirectInput、Gcdef.dll
- ゲーム コントローラ WDK DirectInput、Gcdef.dll
- コントロール パネルの WDK DirectInput、Gcdef.dll
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f35c7b345d28a843fda180dd31f36e3a0ceec614
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388950"
---
# <a name="gcdefdll-the-default-analog-device-property-sheet"></a>Gcdef.dll、既定のアナログ デバイスのプロパティ シート





ハードウェア ベンダーが独自のコントロール パネルを作成しない Gcdef.dll によって提供される既定のアナログ デバイスのプロパティ シートのサービスを使用します。 任意のコント ローラーがない、 **ConfigCLSID**の下のレジストリ キー、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\MediaProperties\\PrivateProperties\\ジョイスティック\\OEM\\**<em>コント ローラー\_名前</em>エントリこの既定のプロパティ シートを使用します。 このプロパティ シートには、次の 2 つのページが含まれています。

-   **テスト:** このページでは、デバイスが正しく応答していることを示します。 デバイスの属性に関連付けられているレジストリ設定のグラフィカル表現を返し、それらを表示するユーザーを許可します。

-   **設定：** このページは、デバイスに関する特定の情報をシステムに書き込むできます。 調整とラダーまたはペダル、サービスが提供されます。

 

 





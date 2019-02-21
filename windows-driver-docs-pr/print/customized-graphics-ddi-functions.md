---
title: カスタマイズされたグラフィックス DDI 関数
description: カスタマイズされたグラフィックス DDI 関数
ms.assetid: 33d7d567-5371-4873-a4ef-cd2b06f65d73
keywords:
- プラグインを WDK の印刷、グラフィックス DDI 関数の表示
- グラフィックス DDI 関数 WDK を印刷します。
- グラフィックス DDI のフック関数 WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeeeaeedfce98e2b4ef4eadbcfa271ee61bd19a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528184"
---
# <a name="customized-graphics-ddi-functions"></a>カスタマイズされたグラフィックス DDI 関数





プリンターのミニドライバーの開発者は、プラグイン メソッドを実装することによってコア プリンターのドライバー グラフィックス Ddi を拡張できます。 プラグインのレンダリングは、一部のグラフィックス中心的なプリンター ドライバーの機能のカスタマイズされた実装を提供する DDI 関数をフックすることできます。 新しいプリンターのレンダリングのプラグインの開発者は、そのプラグインの COM ベースのメソッドを実装する必要があります。参照してください[COM インターフェイスのレンダリング プラグイン](com-interfaces-for-rendering-plug-ins.md)に対して一連の定義済みの COM インターフェイスです。

COM インターフェイスの公開、前に Ihv は、1 つまたは複数の OEM を実装することによってグラフィックス Ddi の機能を拡張できます*Xxx*レンダリング プラグインの関数。互換性の理由からこれらの関数の使用がサポートされていますが、新しいレンダリング プラグインの作成者は、COM インターフェイスでメソッドを使用する必要があります。

このセクションの残りの部分には、次のトピックが含まれています。

[COM ベースのレンダリング プラグイン](com-based-rendering-plug-ins.md)

[COM ベースのレンダリング プラグイン](non-com-based-rendering-plug-ins.md)

 

 





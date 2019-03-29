---
title: 浮動小数点数から XR_BIAS への変換ルール
description: 浮動小数点数から XR_BIAS への変換ルール
ms.assetid: 496306d5-7494-4df6-8af7-9acb0e2708f9
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、XR_BIAS float に変換します。
- 拡張形式 XR_BIAS float に変換する、Windows 7 の WDK の表示
- float に変換する XR_BIAS WDK Windows 7 の表示
- float WDK Windows 7 の表示
- float WDK Windows 7 の表示、XR_BIAS への変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a855d755341496b15157eb769b214087e3f624ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574438"
---
# <a name="float-to-xrbias-conversion-rules"></a>XR に寄せて配置\_バイアス変換規則


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

XR float に変換するため、次の規則が適用\_バイアス。 これらのルールでは、開始の浮動小数点値が c であるとします。

-   C が NaN の場合は、結果は 0 です。それ以外の場合、次の規則が適用されます。 NaN は非数"、"これは、浮動小数点形式で利用できない値を表すシンボルを意味します。

-   スケールの浮動小数点から整数スケールに変換する次の操作を実行します。

    c = c \* 510

    前の操作はオーバーフローを誘発可能性があります。

-   バイアスを次の操作を実行します。

    c = c + 384

    前の操作はオーバーフローを誘発可能性があります。

-   次の操作を c: の指数によって、固定のいずれかを実行します。

    かどうか、post バイアス c のうち指数部が 2 以上 (&gt;2 = c は INF または)、結果は、0x3ff 1.2529 とほぼ同等であります。

    かどうか、post バイアス c のうち指数部が 0 未満です (&lt; 0 または c は、INF)、結果は、「0x0」を表す約-0.7529 します。

-   結果として c の仮数の最上位の 10 ビットを再解釈します。

Float の XR への変換\_バイアスが 0.6f の許容範囲を許可されている単位インプレース最後 (ULP) XR 側でします。 この許容範囲は、XR float 型から変換し後、0.6f 内の任意の値を表す対応のターゲットの形式の値の ULP 許可されているその値にマップするを意味します。 注 1 ULP の無限の正確な結果、たとえば、実装では、結果を 32 ビットを切り捨てることを意味するラウンドでするのに最も近い-なくてを実行するのではなくとエラーになりますの最後 (最下位) に最大で 1 つの単位浮動小数点数で表されます。

データ領域の反転の標準の Direct3D バージョン 10 要件も適用されます。

 

 






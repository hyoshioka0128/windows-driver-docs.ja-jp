---
title: ミニドライバーで指定されるハーフトーン パターン
description: ミニドライバーで指定されるハーフトーン パターン
ms.assetid: db2e1c5c-f337-4875-980d-a75a54a4cece
keywords:
- GDI 指定ハーフトーン WDK Unidrv
- ミニドライバーが指定したハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f97eed9f2072524a51317b8ed2cb8320f41564f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570774"
---
# <a name="minidriver-supplied-halftone-patterns"></a>ミニドライバーで指定されるハーフトーン パターン





ハーフトーンの GDI でサポートされているメソッドを使用しているときに、GDI によりカスタマイズされたハーフトーン パターンの指定を使用できます。 カスタマイズされたハーフトーン パターンを指定するには、次のように使用します。[ハーフトーン機能の属性をオプション](option-attributes-for-the-halftone-feature.md)次のようにします。

-   \*RcHTPatternID、 \*HTPatternSize と\*HTNumPatterns の属性を使用すると、リソース DLL に格納されているハーフトーン パターンについて説明します。 ハーフトーン パターンのリソースは、バイナリ データ、アドレスの DWORD の境界の開始の 3 次元の配列です。 適切なサイズを計算し、必要なアドレスのアラインメントを提供する次の形式を使用して指定できます。

    ```cpp
    BYTE HTPatternResource [HTNumPatterns][(HTPatternSize.y*HTPatternSize.x+3) & ~3];
    ```

    リソース DLL を作成するために使用、.rc ファイル内では、パターンをよう指定可能性があります。

    ```cpp
    1     RC_HTPATTERN LOADONCALL DISCARDABLE HALFTONE.BIN
    ```

    halftone.bin はハーフトーン パターンを含むファイル。

-   \*HTCallbackID 属性を使用するを実装していることを示すために、 [ **IPrintOemUni::HalftonePattern** ](https://msdn.microsoft.com/library/windows/hardware/ff554258)メソッドで、[プラグインをレンダリング](rendering-plug-ins.md). 一意\* **HTCallbackID**パターンごとに値を指定する必要があります、 **IPrintOemUni::HalftonePattern**メソッドがサポートされます。

ハーフトーン パターンのリソースを行うことができます、 **IPrintOemUni::HalftonePattern**メソッド、またはその両方として次のとおりです。

-   ハーフトーン パターンのみを指定する場合、Unidrv はリソース DLL からパターンを取得し、GDI に渡します。 パターンを暗号化することはできません。

-   のみを提供する場合、 **IPrintOemUni::HalftonePattern**メソッド、メソッドする必要があります生成ハーフトーン パターンに戻って Unidrv で、GDI に渡します。

-   リソース DLL で暗号化されたハーフトーン パターンを配置するかどうかは、指定することも必要があります、 **IPrintOemUni::HalftonePattern**メソッド パターンをデコードし、さらに GDI に渡され、Unidrv に戻します。

ハーフトーンの詳細については、[カスタマイズ ハーフトーン](customized-halftoning.md)を参照してください。

 

 





---
title: ミニドライバーで指定されるハーフトーン パターン
description: ミニドライバーで指定されるハーフトーン パターン
ms.assetid: db2e1c5c-f337-4875-980d-a75a54a4cece
keywords:
- GDI が提供するハーフトーン WDK Unidrv
- ミニドライバーが提供するハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f46c94cc711dac24a3680eaa4125936ac3fff1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824270"
---
# <a name="minidriver-supplied-halftone-patterns"></a>ミニドライバーで指定されるハーフトーン パターン





GDI がサポートするハーフトーンメソッドが使用されている場合、GDI は、カスタマイズされたハーフトーンパターンを指定できます。 カスタマイズしたハーフトーンパターンを指定するには、次のように[ハーフトーン機能のオプション属性](option-attributes-for-the-halftone-feature.md)を使用します。

-   \*rcHTPatternID、\*Htpattern の Size 属性と \*Htpatternsize 属性を使用すると、リソース DLL に格納されているハーフトーンパターンを記述できます。 ハーフトーンパターンリソースは、DWORD アドレス境界から始まるバイナリデータの3次元配列です。 次の形式を使用して指定できます。正しいサイズを計算し、必要なアドレスの配置を提供します。

    ```cpp
    BYTE HTPatternResource [HTNumPatterns][(HTPatternSize.y*HTPatternSize.x+3) & ~3];
    ```

    リソース DLL の作成に使用される .rc ファイル内では、パターンは次のように指定できます。

    ```cpp
    1     RC_HTPATTERN LOADONCALL DISCARDABLE HALFTONE.BIN
    ```

    ここで、ハーフビンはハーフトーンパターンを含むファイルです。

-   \*HTCallbackID 属性を使用すると、[レンダリングプラグイン](rendering-plug-ins.md)で[**Iprintoemuni:: HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)メソッドを実装していることを示すことができます。 **Iprintoemuni:: HalftonePattern**メソッドがサポートする各パターンには、一意の \***htcallbackid**値を指定する必要があります。

次のように、ハーフトーンパターンリソース、 **Iprintoemuni:: HalftonePattern**メソッド、またはその両方を指定できます。

-   ハーフトーンパターンだけを指定した場合、Unidrv はリソース DLL からパターンを取得し、それを GDI に渡します。 パターンを暗号化することはできません。

-   **Iprintoemuni:: HalftonePattern**メソッドだけを指定する場合、メソッドは、ハーフトーンパターンを生成して、それを GDI に渡す必要があります。

-   暗号化されたハーフトーンパターンをリソース DLL に配置する場合は、 **Iprintoemuni:: HalftonePattern**メソッドを指定してパターンをデコードし、それらを Unidrv に戻してから、それを GDI に渡します。

ハーフトーンの詳細については、「カスタマイズされた[ハーフトーン](customized-halftoning.md)」を参照してください。

 

 





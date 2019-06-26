---
title: カスタマイズされたハーフトーン
description: カスタマイズされたハーフトーン
ms.assetid: cc14ff92-743b-42ca-b70f-0df768762f01
keywords:
- Unidrv、ハーフトーン
- ハーフトーン WDK Unidrv
- カスタマイズされたハーフトーン WDK Unidrv
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b7d62bd8542cf4caea7570e5d643d40ef294a06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372398"
---
# <a name="customized-halftoning"></a>カスタマイズされたハーフトーン





Unidrv は GDI や、プリンター デバイスを使ってハーフトーン処理を実行することができます。 またはでドライバーのコードをカスタマイズします。 このセクションでは、カスタマイズされたドライバーのコードでハーフトーン処理を実行する方法について説明します。

カスタマイズの 2 つの種類があります。

-   カスタマイズされたハーフトーン パターン

-   カスタマイズされたハーフトーン メソッド

### <a href="" id="ddk-customized-halftone-patterns-gg"></a>カスタマイズされたハーフトーン パターン

ハーフトーン パターンを指定するにはリソース DLL を生成したりできますにプラグインを表示して実装する、 [ **IPrintOemUni::HalftonePattern** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)メソッド。 このメソッドのリファレンス ページは、ハーフトーン パターンを生成する方法の例を示します。

[**IPrintOemUni::HalftonePattern** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)次のいずれかが true の場合に実装する必要があります。

-   カスタマイズされたパターンがリソース DLL で提供されており、パターンが暗号化されます。

-   カスタマイズしたパターンは、リソース DLL では提供されません。 によって生成される代わりに、 [ **IPrintOemUni::HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)します。

[ **IPrintOemUni::HalftonePattern** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)メソッドの目的を GDI に渡されます Unidrv に使用可能なハーフトーン パターンを返します。 メソッドは、暗号化された形式でのリソース DLL に格納されているパターンをデコードできるか、または実行中に、パターンを生成できます。

実装する場合、 **IPrintOemUni::HalftonePattern**ファイルを含める必要があります、\*各ハーフトーン HTCallbackID 属性\*なカスタマイズされたパターンのハーフトーン メソッドを指定したエントリのオプションこのオプションを使用するとします。

この属性の詳細については、次を参照してください。[ハーフトーン機能のオプション属性](option-attributes-for-the-halftone-feature.md)します。

### <a href="" id="ddk-customized-halftoning-methods-gg"></a>カスタマイズされたハーフトーン メソッド

Unidrv を使用するプリンター、カスタマイズしたハーフトーン メソッドを実装するコードを提供する手順は次のとおりです。

1.  実装するプラグインのレンダリングを提供、 [ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッド。

2.  含めるハーフトーン\*に含まれている各プリンターの GPD ファイル内のエントリを機能\*ハーフトーン メソッドを表すエントリのオプションします。 (Standard、およびカスタマイズされたハーフトーン メソッド両方に指定できます。)

[ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドは入力として GDI ビットマップを受け取ります。 メソッドは、現在選択されているハーフトーン メソッドに基づいて、ハーフトーン操作を実行し、Unidrv に、結果のビットマップを返す必要があります。

レンダリングのプラグインを実装する場合[ **IPrintOemUni::ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)も実装できます、 [ **IPrintOemUni::MemoryUsage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-memoryusage).

ハーフトーンの詳細については、次を参照してください。 [Unidrv のハーフトーン](halftoning-with-unidrv.md)します。

 

 





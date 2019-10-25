---
title: カスタマイズされたハーフトーン
description: カスタマイズされたハーフトーン
ms.assetid: cc14ff92-743b-42ca-b70f-0df768762f01
keywords:
- Unidrv、ハーフトーン
- ハーフトーン WDK Unidrv
- カスタマイズされたハーフトーン WDK Unidrv
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4555984f5d15bebd98353c4f3c944785aa57974c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837976"
---
# <a name="customized-halftoning"></a>カスタマイズされたハーフトーン





Unidrv では、GDI、プリンターデバイス、またはカスタマイズされたドライバーコードを使用して、ハーフトーン操作を実行できます。 このセクションでは、カスタマイズされたドライバーコードでハーフトーン操作を実行する方法について説明します。

2種類のカスタマイズが用意されています。

-   カスタマイズされたハーフトーンパターン

-   カスタマイズされたハーフトーンメソッド

### <a href="" id="ddk-customized-halftone-patterns-gg"></a>カスタマイズされたハーフトーンパターン

リソース DLL でハーフトーンパターンを指定することも、 [**Iprintoemuni:: HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)メソッドを実装するレンダリングプラグインでそれらを生成することもできます。 このメソッドのリファレンスページでは、ハーフトーンパターンを生成する方法の例を示します。

次のいずれかに該当する場合は、 [**Iprintoemuni:: HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)を実装する必要があります。

-   カスタマイズしたパターンはリソース DLL で提供され、パターンは暗号化されます。

-   リソース DLL では、カスタマイズされたパターンは提供されません。 代わりに、 [**Iprintoemuni:: HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)によって生成されます。

[**Iprintoemuni:: HalftonePattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)メソッドの目的は、使用可能なハーフトーンパターンを Unidrv に戻し、さらにそれを GDI に渡すことです。 メソッドは、リソース DLL に格納されているパターンを暗号化された形式でデコードするか、実行中にパターンを生成することができます。

**Iprintoemuni:: HalftonePattern**ファイルを実装する場合は、カスタマイズされたパターンを使用するハーフトーン方式を指定する \*オプションのエントリを各ハーフトーンに \*HTCallbackID 属性を含める必要があります。

この属性の詳細については、「[ハーフトーン機能のオプション属性](option-attributes-for-the-halftone-feature.md)」を参照してください。

### <a href="" id="ddk-customized-halftoning-methods-gg"></a>カスタマイズされたハーフトーンメソッド

Unidrv を使用するプリンターでは、カスタマイズされたハーフトーンメソッドを実装するコードを提供する手順は次のとおりです。

1.  [**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドを実装するレンダリングプラグインを提供します。

2.  プリンターの GPD ファイルにハーフトーン \*機能のエントリを含めます。それぞれに、ハーフトーン方式を表す \*オプションのエントリが含まれています。 (標準およびカスタマイズされたハーフトーン方式の両方を含めることができます)。

[**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドは、GDI ビットマップを入力として受け取ります。 メソッドは、現在選択されているハーフトーンメソッドに基づいてハーフトーン操作を実行し、結果のビットマップを Unidrv に返す必要があります。

レンダリングプラグインが[**iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)を実装している場合は、 [**Iprintoemuni:: memoryusage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)を実装することもできます。

ハーフトーンの詳細については、「 [Unidrv によるハーフトーン](halftoning-with-unidrv.md)」を参照してください。

 

 





---
title: IPrintOemUni3 COM インターフェイス
description: IPrintOemUni3 COM インターフェイス
ms.assetid: 2b3a43fe-52f8-4cb2-993e-d8fcdc878e90
keywords:
- IPrintOemUni3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ccde661bc647be33a0c395cc0d3fa7639909a1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841764"
---
# <a name="iprintoemuni3-com-interface"></a>IPrintOemUni3 COM インターフェイス





`IPrintOemUni3` COM インターフェイスには、のすべてのメソッドが含まれています。また、 [Iprintoemuni Com インターフェイス](iprintoemuni-com-interface.md)と[IPrintOemUni2 com インターフェイス](iprintoemuni2-com-interface.md)の機能が拡張されています。

次の表に、`IPrintOemUni3` インターフェイスによって提供されるすべてのメソッドとその説明を示します。 レンダリングプラグインでは、表示されているすべてのメソッドを定義する必要があります。 メソッドが不要な場合は、単に E\_NOTIMPL を返すことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern" data-raw-source="[&lt;strong&gt;IPrintOemUni3::DownloadPattern&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-downloadpattern)"><strong>IPrintOemUni3::D ownloadPattern</strong></a></p></td>
<td><p>プラグインを使用してプリンターにパターンをダウンロードできるようにします。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment" data-raw-source="[&lt;strong&gt;IPrintOemUni3::GetPDEVAdjustment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-getpdevadjustment)"><strong>IPrintOemUni3:: GetPDEVAdjustment</strong></a></td>
<td><p>プラグインが特定の<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"><em>Pdev</em></a>設定をオーバーライドできるようにします。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize" data-raw-source="[&lt;strong&gt;IPrintOemUni3::SetBandSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni3-setbandsize)"><strong>IPrintOemUni3:: Setバンドサイズ</strong></a></td>
<td><p>プラグインを使用して、印刷出力に必要な帯域幅を指定できるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 





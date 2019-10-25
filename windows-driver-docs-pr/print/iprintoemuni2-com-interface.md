---
title: IPrintOemUni2 COM インターフェイス
description: IPrintOemUni2 COM インターフェイス
ms.assetid: 7dabc133-a77c-43af-9171-1195fcaf3162
keywords:
- IPrintOemUni2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd0e0ca712c93d1795042fa7f19d74ba9212083f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841768"
---
# <a name="iprintoemuni2-com-interface"></a>IPrintOemUni2 COM インターフェイス





`IPrintOemUni2` COM インターフェイスには、のすべてのメソッドが含まれています。また、 [Iprintoemuni COM インターフェイス](iprintoemuni-com-interface.md)の機能が拡張されています。

次の表に、`IPrintOemUni2` インターフェイスによって提供されるすべてのメソッドとその説明を示します。 レンダリングプラグインでは、表示されているすべてのメソッドを定義する必要があります。 メソッドが不要な場合は、単に E\_NOTIMPL を返すことができます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUni2::WritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter)"><strong>IPrintOemUni2:: WritePrinter</strong></a></p></td>
<td><p>プラグインが、Unidrv ドライバーによって生成されたすべての出力データをキャプチャできるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 





---
title: IPrintOemUIMXDC COM インターフェイス
description: IPrintOemUIMXDC COM インターフェイス
ms.assetid: db6d575e-31d0-4a26-8cf9-5188935610e5
keywords:
- IPrintOemUIMXDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d04b164d87926c7a923a8b81bf1dbb07fc030d06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842302"
---
# <a name="iprintoemuimxdc-com-interface"></a>IPrintOemUIMXDC COM インターフェイス


`IPrintOemUIMXDC` COM インターフェイスを使用すると、XPS フィルターパイプラインドライバーは、プリンターの構成用の[プリンターインターフェイス DLL](printer-interface-dll.md)によって管理される情報を表示および変更できます。 XPS ドライバーは、 [Unidrv または Pscript プラグイン](xpsdrv-driver-options.md)を介してこの COM インターフェイスにアクセスします。

次の表に、`IPrintOemUIMXDC` インターフェイスで定義されているすべてのメソッドの一覧とその説明を示します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageableArea&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea)"><strong>IPrintOEMUIMXDC::AdjustImageableArea</strong></a></p></td>
<td><p>XPS フィルターパイプラインドライバーが UnidrvUI または PS5UI を使用して、回転の向きや向きなど、印刷可能領域の構成をサポートできるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageCompression&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression)"><strong>IPrintOEMUIMXDC::AdjustImageCompression</strong></a></p></td>
<td><p>XPS フィルターパイプラインドライバーが、JPEG イメージの圧縮レベルの構成をサポートするために UnidrvUI または PS5UI を使用できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustDPI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi)"><strong>IPrintOEMUIMXDC::AdjustDPI</strong></a></p></td>
<td><p>XPS フィルターパイプラインドライバーが、イメージの解像度の構成をサポートするために UnidrvUI または PS5UI を使用できるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 





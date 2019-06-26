---
title: IPrintOemUIMXDC COM インターフェイス
description: IPrintOemUIMXDC COM インターフェイス
ms.assetid: db6d575e-31d0-4a26-8cf9-5188935610e5
keywords:
- IPrintOemUIMXDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eb9ec92512289fa3bd2c05446ce5cb5ac95555d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371750"
---
# <a name="iprintoemuimxdc-com-interface"></a>IPrintOemUIMXDC COM インターフェイス


`IPrintOemUIMXDC` COM インターフェイスにより、情報を表示したり、XPS フィルター パイプラインのドライバーを[プリンター インターフェイス DLL](printer-interface-dll.md)のプリンター構成を管理します。 XPS ドライバーを通じてこの COM インターフェイスにアクセスする、 [Unidrv またはプラグイン Pscript](xpsdrv-driver-options.md)します。

次の表に、すべてのメソッドを示し、`IPrintOemUIMXDC`インターフェイスを定義します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageableArea&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimageablearea)"><strong>IPrintOEMUIMXDC::AdjustImageableArea</strong></a></p></td>
<td><p>UnidrvUI.dll または PS5UI.dll を使用して、向き、回転の方向など、印刷可能領域の構成をサポートする XPS フィルター パイプライン ドライバーを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustImageCompression&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustimagecompression)"><strong>IPrintOEMUIMXDC::AdjustImageCompression</strong></a></p></td>
<td><p>UnidrvUI.dll または PS5UI.dll を使用して、JPEG 画像の圧縮レベルの構成をサポートする XPS フィルター パイプライン ドライバーを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi" data-raw-source="[&lt;strong&gt;IPrintOEMUIMXDC::AdjustDPI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuimxdc-adjustdpi)"><strong>IPrintOEMUIMXDC::AdjustDPI</strong></a></p></td>
<td><p>UnidrvUI.dll または PS5UI.dll を使用して、画像の解像度の構成をサポートする XPS フィルター パイプライン ドライバーを有効にします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 





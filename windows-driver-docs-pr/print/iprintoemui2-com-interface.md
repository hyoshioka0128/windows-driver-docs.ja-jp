---
title: IPrintOemUI2 COM インターフェイス
description: IPrintOemUI2 COM インターフェイス
ms.assetid: 9aee61af-e8e2-4bc4-a17b-783242d1ac1f
keywords:
- IPrintOemUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67cad985aaefdcd113809dec7952a9426d60da9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371762"
---
# <a name="iprintoemui2-com-interface"></a>IPrintOemUI2 COM インターフェイス





`IPrintOemUI2` COM インターフェイスは、拡張、 [IPrintOemUI COM インターフェイス](iprintoemui-com-interface.md)します。 すべてのメソッドだけでなく、 **IPrintOemUI**インターフェイス、`IPrintOemUI2`インターフェイスは、次のメソッドを提供します。

**注**  Unidrv と Pscript Dll の Windows Vista のバージョンを使用している場合は、Unidrv または Pscript5 プラグインで Windows XP およびそれ以降のバージョンの Windows オペレーティング システムで実行される、次のメソッドを実装できます。 以前のバージョンの Dll のサポート、 **IPrintOEM2::HideStandardUI** Pscript5 プラグインのみでのメソッド。

 

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-documentevent" data-raw-source="[&lt;strong&gt;IPrintOemUI2::DocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-documentevent)"><strong>IPrintOemUI2::DocumentEvent</strong></a></p></td>
<td><p>により、UI プラグインのコア ドライバー UI モジュールの既定の実装を置き換える、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent)"> <strong>DrvDocumentEvent</strong> </a> DDI します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui" data-raw-source="[&lt;strong&gt;IPrintOemUI2::HideStandardUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui)"><strong>IPrintOemUI2::HideStandardUI</strong></a></p></td>
<td><p>標準のプロパティ シートを表示または非表示かどうかを指定する UI プラグインを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes" data-raw-source="[&lt;strong&gt;IPrintOemUI2::QueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes)"><strong>IPrintOemUI2::QueryJobAttributes</strong></a></p></td>
<td><p>により、処理後の呼び出しの後に、中核となるドライバーの結果を UI プラグイン、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvqueryjobattributes" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvqueryjobattributes)"> <strong>DrvQueryJobAttributes</strong> </a> DDI します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 





---
title: IPrintOemUI2 COM インターフェイス
description: IPrintOemUI2 COM インターフェイス
ms.assetid: 9aee61af-e8e2-4bc4-a17b-783242d1ac1f
keywords:
- IPrintOemUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3f98e195d2b4ea21004b013a28df8d64f88003c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837856"
---
# <a name="iprintoemui2-com-interface"></a>IPrintOemUI2 COM インターフェイス





`IPrintOemUI2` COM インターフェイスは、 [Iprintoemui com インターフェイス](iprintoemui-com-interface.md)を拡張します。 **Iprintoemui**インターフェイスのすべてのメソッドに加えて、`IPrintOemUI2` インターフェイスには次のメソッドが用意されています。

**注**  windows Vista バージョンの Unidrv および Pscript dll を使用している場合は、windows XP 以降のバージョンの windows オペレーティングシステムで実行される unidrv または Pscript5 プラグインで、次のメソッドを実装できます。 以前のバージョンの Dll では、Pscript5 プラグインでのみ**IPrintOEM2:: HideStandardUI**メソッドがサポートされています。

 

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-documentevent" data-raw-source="[&lt;strong&gt;IPrintOemUI2::DocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-documentevent)"><strong>IPrintOemUI2::D ocumentEvent</strong></a></p></td>
<td><p>UI プラグインを使用して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent)"><strong>DrvDocumentEvent</strong></a> DDI のコアドライバー ui モジュールの既定の実装を置き換えることができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui" data-raw-source="[&lt;strong&gt;IPrintOemUI2::HideStandardUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui)"><strong>IPrintOemUI2::HideStandardUI</strong></a></p></td>
<td><p>標準プロパティシートを表示するか非表示にするかを UI プラグインで指定できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes" data-raw-source="[&lt;strong&gt;IPrintOemUI2::QueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes)"><strong>IPrintOemUI2:: QueryJobAttributes</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes)"><strong>DrvQueryJobAttributes</strong></a> DDI の呼び出し後に、UI プラグインがコアドライバーの結果を後処理できるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 





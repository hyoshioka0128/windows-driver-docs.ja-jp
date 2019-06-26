---
title: IPrintOemPS2 COM インターフェイス
description: IPrintOemPS2 COM インターフェイス
ms.assetid: 6743d73e-243b-4a05-8e88-576c65b37a19
keywords:
- IPrintOemPS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64fe0c66d523ed99d412a64537aafb239e687eab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386948"
---
# <a name="iprintoemps2-com-interface"></a>IPrintOemPS2 COM インターフェイス





`IPrintOemPS2` COM インターフェイスのすべてのメソッドが含まれていますとの機能を拡張、 [IPrintOemPS COM インターフェイス](iprintoemps-com-interface.md)します。 このインターフェイスは、Windows XP およびそれ以降のバージョンの Windows オペレーティング システムで実行される Pscript5 レンダリング プラグインに制限されます。

次の表とによって提供されるメソッドのすべてについて説明します、`IPrintOemPS2`インターフェイス。 プラグインを表示、表示されているすべてのメソッドを定義する必要があります。 かどうか、メソッドは必要ありません、単に返すことができます E\_NOTIMPL します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps2-getpdevadjustment" data-raw-source="[&lt;strong&gt;IPrintOemPS2::GetPDEVAdjustment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps2-getpdevadjustment)"><strong>IPrintOemPS2::GetPDEVAdjustment</strong></a></p></td>
<td><p>特定の PDEV 設定を上書きするプラグインを使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemPS2::WritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps2-writeprinter)"><strong>IPrintOemPS2::WritePrinter</strong></a></p></td>
<td><p>Postscript ドライバーによって生成されたすべての出力データをキャプチャするプラグインを使用できます。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 





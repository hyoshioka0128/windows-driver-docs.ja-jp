---
title: IPrintOemPS2 COM インターフェイス
description: IPrintOemPS2 COM インターフェイス
ms.assetid: 6743d73e-243b-4a05-8e88-576c65b37a19
keywords:
- IPrintOemPS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd2b08c5878ec785db631ab50860dee9bdd6e3f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837859"
---
# <a name="iprintoemps2-com-interface"></a>IPrintOemPS2 COM インターフェイス





`IPrintOemPS2` COM インターフェイスには、のすべてのメソッドが含まれており、 [IPRINTOEMPS Com インターフェイス](iprintoemps-com-interface.md)の機能が拡張されています。 このインターフェイスは、Windows XP 以降のバージョンの Windows オペレーティングシステムで動作する Pscript5 レンダリングプラグインに限定されています。

次の表に、`IPrintOemPS2` インターフェイスによって提供されるすべてのメソッドとその説明を示します。 レンダリングプラグインでは、表示されているすべてのメソッドを定義する必要があります。 メソッドが不要な場合は、単に E\_NOTIMPL を返すことができます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-getpdevadjustment" data-raw-source="[&lt;strong&gt;IPrintOemPS2::GetPDEVAdjustment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-getpdevadjustment)"><strong>IPrintOemPS2:: GetPDEVAdjustment</strong></a></p></td>
<td><p>プラグインが特定の PDEV 設定をオーバーライドできるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-writeprinter" data-raw-source="[&lt;strong&gt;IPrintOemPS2::WritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps2-writeprinter)"><strong>IPrintOemPS2:: WritePrinter</strong></a></p></td>
<td><p>プラグインが Postscript ドライバーによって生成されたすべての出力データをキャプチャできるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 





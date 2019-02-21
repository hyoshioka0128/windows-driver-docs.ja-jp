---
title: IPrintOemUI2 COM インターフェイス
description: IPrintOemUI2 COM インターフェイス
ms.assetid: 9aee61af-e8e2-4bc4-a17b-783242d1ac1f
keywords:
- IPrintOemUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51b063e79ca31f950dc7f31e525f085f7403e8a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558852"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554141" data-raw-source="[&lt;strong&gt;IPrintOemUI2::DocumentEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554141)"><strong>IPrintOemUI2::DocumentEvent</strong></a></p></td>
<td><p>により、コア ドライバーの UI モジュールを交換する UI プラグイン&#39;s の既定の実装、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548544" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548544)"> <strong>DrvDocumentEvent</strong> </a> DDI します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554142" data-raw-source="[&lt;strong&gt;IPrintOemUI2::HideStandardUI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554142)"><strong>IPrintOemUI2::HideStandardUI</strong></a></p></td>
<td><p>標準のプロパティ シートを表示または非表示かどうかを指定する UI プラグインを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554146" data-raw-source="[&lt;strong&gt;IPrintOemUI2::QueryJobAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554146)"><strong>IPrintOemUI2::QueryJobAttributes</strong></a></p></td>
<td><p>により、処理後の中核となるドライバーに UI プラグイン&#39;s 結果への呼び出しの後、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548581" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548581)"> <strong>DrvQueryJobAttributes</strong> </a> DDI します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 





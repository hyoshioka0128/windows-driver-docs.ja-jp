---
title: IPrintOemUni3 COM インターフェイス
description: IPrintOemUni3 COM インターフェイス
ms.assetid: 2b3a43fe-52f8-4cb2-993e-d8fcdc878e90
keywords:
- IPrintOemUni3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e28efbddce1f27e6dd20af41fdd6e1ff5c3ef2b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528750"
---
# <a name="iprintoemuni3-com-interface"></a>IPrintOemUni3 COM インターフェイス





`IPrintOemUni3` COM インターフェイスは、のすべてのメソッドが含まれていての機能を拡張、 [IPrintOemUni COM インターフェイス](iprintoemuni-com-interface.md)と[IPrintOemUni2 COM インターフェイス](iprintoemuni2-com-interface.md)します。

次の表とによって提供されるメソッドのすべてについて説明します、`IPrintOemUni3`インターフェイス。 プラグインをレンダリングと、一覧内のすべてのメソッドを定義する必要があります。 かどうか、メソッドは必要ありません、単に返すことができます E\_NOTIMPL します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554201" data-raw-source="[&lt;strong&gt;IPrintOemUni3::DownloadPattern&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554201)"><strong>IPrintOemUni3::DownloadPattern</strong></a></p></td>
<td><p>パターンをプリンターにダウンロードするプラグインを使用できます。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff554205" data-raw-source="[&lt;strong&gt;IPrintOemUni3::GetPDEVAdjustment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554205)"><strong>IPrintOemUni3::GetPDEVAdjustment</strong></a></td>
<td><p>プラグインを特定のオーバーライドにより<a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"> <em>PDEV</em> </a>設定します。</p></td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff554209" data-raw-source="[&lt;strong&gt;IPrintOemUni3::SetBandSize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554209)"><strong>IPrintOemUni3::SetBandSize</strong></a></td>
<td><p>により、印刷出力で必要なバンド サイズを指定するプラグイン</p></td>
</tr>
</tbody>
</table>

 

詳細については、[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)を参照してください。

 

 





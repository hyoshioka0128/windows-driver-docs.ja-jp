---
title: IPrintCorePS2 COM インターフェイス
description: IPrintCorePS2 COM インターフェイス
ms.assetid: d5eb6962-2201-405f-9a22-2b11fb6d0360
keywords:
- IPrintCorePS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ffdaddd7512087c532e2b98568144fd8325bdc3
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348913"
---
# <a name="iprintcoreps2-com-interface"></a>IPrintCorePS2 COM インターフェイス





`IPrintCorePS2` Pscript5 レンダリング プラグインの COM インターフェイスが一連のヘルパー メソッドを提供します。次の表とによって定義されたメソッドのすべてについて説明します、`IPrintCorePS2`インターフェイス。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552978" data-raw-source="[&lt;strong&gt;IPrintCorePS2::DrvWriteSpoolBuf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552978)"><strong>IPrintCorePS2::DrvWriteSpoolBuf</strong></a></p></td>
<td><p>Pscript5 ドライバーによって提供されるように<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-ins](rendering-plug-ins.md)">レンダリング プラグイン</a>スプーラーにプリンターのデータを送信することができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552990" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumFeatures&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552990)"><strong>IPrintCorePS2::EnumFeatures</strong></a></p></td>
<td><p>プリンターの使用可能な機能を列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552996" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552996)"><strong>IPrintCorePS2::EnumOptions</strong></a></p></td>
<td><p>特定の機能の使用可能なオプションを列挙します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553006" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetFeatureAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553006)"><strong>IPrintCorePS2::GetFeatureAttribute</strong></a></p></td>
<td><p>機能の属性リストまたは特定の機能の属性の値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553009" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetGlobalAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553009)"><strong>IPrintCorePS2::GetGlobalAttribute</strong></a></p></td>
<td><p>グローバル属性の一覧または特定のグローバル属性の値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553013" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptionAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553013)"><strong>IPrintCorePS2::GetOptionAttribute</strong></a></p></td>
<td><p>オプションの属性リストまたは特定のオプションの属性の値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553019" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553019)"><strong>IPrintCorePS2::GetOptions</strong></a></p></td>
<td><p>ドライバーの機能またはオプションのキーワードの組み合わせの一覧の形式で現在機能の設定を取得します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 





---
title: IPrintCorePS2 COM インターフェイス
description: IPrintCorePS2 COM インターフェイス
ms.assetid: d5eb6962-2201-405f-9a22-2b11fb6d0360
keywords:
- IPrintCorePS2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57794352cb5908e9f9db3939b043ddfad402228b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386305"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-drvwritespoolbuf" data-raw-source="[&lt;strong&gt;IPrintCorePS2::DrvWriteSpoolBuf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-drvwritespoolbuf)"><strong>IPrintCorePS2::DrvWriteSpoolBuf</strong></a></p></td>
<td><p>Pscript5 ドライバーによって提供されるように<a href="rendering-plug-ins.md" data-raw-source="[rendering plug-ins](rendering-plug-ins.md)">レンダリング プラグイン</a>スプーラーにプリンターのデータを送信することができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumFeatures&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures)"><strong>IPrintCorePS2::EnumFeatures</strong></a></p></td>
<td><p>プリンターの使用可能な機能を列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions" data-raw-source="[&lt;strong&gt;IPrintCorePS2::EnumOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions)"><strong>IPrintCorePS2::EnumOptions</strong></a></p></td>
<td><p>特定の機能の使用可能なオプションを列挙します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetFeatureAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute)"><strong>IPrintCorePS2::GetFeatureAttribute</strong></a></p></td>
<td><p>機能の属性リストまたは特定の機能の属性の値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetGlobalAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute)"><strong>IPrintCorePS2::GetGlobalAttribute</strong></a></p></td>
<td><p>グローバル属性の一覧または特定のグローバル属性の値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptionAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute)"><strong>IPrintCorePS2::GetOptionAttribute</strong></a></p></td>
<td><p>オプションの属性リストまたは特定のオプションの属性の値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptions" data-raw-source="[&lt;strong&gt;IPrintCorePS2::GetOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptions)"><strong>IPrintCorePS2::GetOptions</strong></a></p></td>
<td><p>ドライバーの機能またはオプションのキーワードの組み合わせの一覧の形式で現在機能の設定を取得します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 





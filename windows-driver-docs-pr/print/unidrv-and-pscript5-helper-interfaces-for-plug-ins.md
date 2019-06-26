---
title: プラグインの Unidrv と Pscript5 ヘルパーのインターフェイス
description: プラグインの Unidrv と Pscript5 ヘルパーのインターフェイス
ms.assetid: 043a38f7-200c-4f1d-b937-4ddd6e2045dd
keywords:
- IPrintCoreHelperPS
- IPrintCoreHelperUni
- IPrintCoreHelper
- ヘルパー インターフェイス WDK プリンター インターフェイス DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68ebf1d245e9d043e14293091c517e9b4843c941
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378592"
---
# <a name="unidrv-and-pscript5-helper-interfaces-for-plug-ins"></a>プラグインの Unidrv と Pscript5 ヘルパーのインターフェイス


[IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)と[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)インターフェイスの継承、 [IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelper)インターフェイス、3 つすべてのインターフェイスがの共通のセットを共有します。メソッド。 次の表では、ヘルパーのインターフェイスとメモが、方法を次の 3 つのすべてのインターフェイスで使用可能なとが、方法をインターフェイスの 1 つのみで使用可能なメソッドを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>含まれています。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConvertStringToPTFormat</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="even">
<td><p><strong>ConvertDefaultGDLSnapshot</strong></p></td>
<td><p><strong>IPrintCoreHelperUni</strong>のみインターフェイス</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConvertGDLSnapshot</strong></p></td>
<td><p><strong>IPrintCoreHelperUni</strong>のみインターフェイス</p></td>
</tr>
<tr class="even">
<td><p><strong>CreateInstanceOfMSXMLObject</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumConstrainedOptions</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumFeatures</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumOptions</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="even">
<td><p><strong>GetFeatureAttribute</strong></p></td>
<td><p><strong>IPrintCoreHelperPS</strong>のみインターフェイス</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetGlobalAttribute</strong></p></td>
<td><p><strong>IPrintCoreHelperPS</strong>のみインターフェイス</p></td>
</tr>
<tr class="even">
<td><p><strong>GetOptionAttribute</strong></p></td>
<td><p><strong>IPrintCoreHelperPS</strong>のみインターフェイス</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetOption</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="even">
<td><p><strong>SetOptions</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="odd">
<td><p><strong>WhyConstrained</strong></p></td>
<td><p>すべての</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: プラグインの Unidrv と Pscript5 ヘルパーのインターフェイス
description: プラグインの Unidrv と Pscript5 ヘルパーのインターフェイス
ms.assetid: 043a38f7-200c-4f1d-b937-4ddd6e2045dd
keywords:
- Iprintcoreの Perps
- Iprintcoreの Peruni
- IPrintCoreHelper
- ヘルパーインターフェイス WDK プリンターインターフェイス DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38db3f592fc39b4372e909576ad52fb184d2eb91
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845239"
---
# <a name="unidrv-and-pscript5-helper-interfaces-for-plug-ins"></a>プラグインの Unidrv と Pscript5 ヘルパーのインターフェイス


[Iprintcoreの Perps](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)インターフェイスと[iprintcoreの](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)インターフェイスは[iprintcorehelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)インターフェイスから継承されるため、3つのすべてのインターフェイスは、共通のメソッドのセットを共有します。 次の表は、ヘルパーインターフェイスのメソッドの一覧です。3つのインターフェイスすべてで使用できるメソッドと、1つのインターフェイスで使用できるメソッドについて説明しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>含まれている</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConvertStringToPTFormat</strong></p></td>
<td><p>すべての</p></td>
</tr>
<tr class="even">
<td><p><strong>ConvertDefaultGDLSnapshot</strong></p></td>
<td><p><strong>Iprintcoreの Peruni</strong>インターフェイスのみ</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConvertGDLSnapshot</strong></p></td>
<td><p><strong>Iprintcoreの Peruni</strong>インターフェイスのみ</p></td>
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
<td><p><strong>Iprintcoreの Perps</strong>インターフェイスのみ</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetGlobalAttribute</strong></p></td>
<td><p><strong>Iprintcoreの Perps</strong>インターフェイスのみ</p></td>
</tr>
<tr class="even">
<td><p><strong>GetOptionAttribute</strong></p></td>
<td><p><strong>Iprintcoreの Perps</strong>インターフェイスのみ</p></td>
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

 

 

 




